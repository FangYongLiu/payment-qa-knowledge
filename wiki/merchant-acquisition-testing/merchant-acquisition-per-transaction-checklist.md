---
title: 每笔交易检查清单
domain: merchant-acquisition-testing
kind: wiki_page
slug: merchant-acquisition-per-transaction-checklist
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:AQ/2125922317
tags: []
---

# 每笔交易检查清单

每跑完一笔交易，按下面五段顺序逐项打钩；任何一段未确认都不算"测过"。这份清单是 [[merchant-acquisition-e2e-five-stage-verification]] 的可执行落地版本，建议打印或贴到任务卡片上。

## ① 接口响应

- [ ] HTTP 200，`applyStatus=SUCCESS`，`head.code=0`，`status` 符合场景预期
- [ ] 错误用例：错误码与场景对应（见 [[merchant-acquisition-error-code-cheatsheet]]）
- [ ] 注意 `applyStatus=SUCCESS` 不等于业务成功，必须看 `code` 和 `body.acquireOrder.status`

## ② 服务调用链

- [ ] `traceCode` 全链路日志可查，每个服务（sgs / acquireii / cashierii / authPay / cmf / router / qpay-mpgs 等）都打到
- [ ] 关键参数正确（如 PreAuth 的 `apiOperation=AUTHORIZE` 而非 `PAY`）
- [ ] 渠道侧请求：apiOperation、路由码、子商户 ID 正确
- [ ] 无 5xx、无重试堆叠、无超时

## ③ 数据库落库

- [ ] 该落库的表都有记录（acquireii / tradeii / cmf / payment / reconciliation 等按场景核对）
- [ ] 新增/更新行数符合预期，不多不少
- [ ] 状态字段流转符合状态机
- [ ] 金额字段（totalAmount / dccAmount / capture amount）正确
- [ ] 跨表关联字段一致：`merchantOrderNo` / `paymentSeqNo` / `preauthOrderNo`

## ④ Fund Flow

- [ ] 该产生入账流水的场景（支付成功 / Capture / Refund）：`t_fund_flow` 有记录
- [ ] 借贷平衡：每组分录 Total Dr = Total Cr
- [ ] 账户方向正确：Fund-In Pending / Merchant Pending / Merchant Basic / Payby Revenue
- [ ] 不该产生流水的场景（CREATED 未支付 / 支付失败 / PreAuth 仅冻结 / Void）：确认 `t_fund_flow` 确实没有记录 ⭐

## ⑤ 通知 & 对账

- [ ] `notifyUrl` 收到 POST，body 字段完整（notify_id / notify_timestamp / 订单对象）
- [ ] 商户回 `{"response":"SUCCESS"}` + HTTP 200 + `application/json` 后不再重试
- [ ] 模拟非 SUCCESS / 非 200 / 超时：重试时间表（2→10→10→60→120→360→900 分钟，共 7 次）符合预期
- [ ] T+1 对账单 ZIP 下载到，包含 Transaction / Settlement / Fund Statement 三类 CSV
- [ ] 本笔在对账单中类型与金额正确（PreAuth 不进对账单，Capture 才进；Revoke 显示为 `REVERTED`）
- [ ] 详见 [[merchant-acquisition-notify-statement-spec]]

## 横切补充：边界与安全

按 [[merchant-acquisition-test-case-skeleton-abcde]] 的 D / E 组覆盖：

- [ ] 幂等：同 `merchantOrderNo` 重复下单
- [ ] 跨日：23:59 创建、0:01 通知
- [ ] 并发：同单高并发下单
- [ ] 签名异常：sign 错误 / Partner-Id 错误 → 403
- [ ] 时间戳偏差 > 15 分钟 → `REQUESTTIME_TOO_EARLY/LATER`
- [ ] 权限缺失：未开通产品包 → `62026 PRODUCT_IS_NOT_APPLIED`
- [ ] 跨商户使用 `cardToken` / `preauthOrderNo` → `Invalid partner id`

## 配套资料

- 调用骨架与签名 Header：[[merchant-acquisition-curl-postman-templates]]
- 测试卡 / 金额 / `merchantOrderNo` 命名：[[merchant-acquisition-test-data-preparation]]
- 环境域名 / MID / 数据库入口：[[merchant-acquisition-test-environment-tools]]
- 方法论总览：[[merchant-acquisition-test-methodology-overview]]
