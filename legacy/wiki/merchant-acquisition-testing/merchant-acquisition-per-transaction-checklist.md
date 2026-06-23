---
title: 每笔交易检查清单
domain: merchant-acquisition-testing
kind: wiki_page
slug: merchant-acquisition-per-transaction-checklist
status: archived
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:AQ/2125922317
tags: []
---

# 每笔交易测试检查清单

> 每跑完一笔交易,按下面五段顺序逐项打 ✓;任何一段未确认都不算"测过"。可直接贴到任务卡片或 PR 描述里。本清单是 [[merchant-acquisition-e2e-five-stage-verification]] 的浓缩可执行落地版本。

## ① 接口响应

- [ ] HTTP 200
- [ ] `head.applyStatus = SUCCESS`
- [ ] `head.code = 0`
- [ ] `body` 中订单状态符合预期(`CREATED` / `PAID_SUCCESS` / `AUTHORIZATION` 等),即 `body.acquireOrder.status` 与场景一致
- [ ] 异常用例:错误码与场景对应(见 [[merchant-acquisition-error-code-quickref]] / [[merchant-acquisition-error-code-cheatsheet]])
- [ ] 注意:`applyStatus=SUCCESS` ≠ 业务成功,必看 `code` 与 `body.acquireOrder.status`

## ② 服务调用链

- [ ] 用 `traceCode` 全链路日志可查
- [ ] 每个相关服务都有日志(sgs / acquireii / cashierii / authPay / cmf / router / qpay-mpgs 等),无日志 = 未调到
- [ ] 关键参数正确:例如 PreAuth 的 MPGS `apiOperation = AUTHORIZE`(不是 `PAY`)
- [ ] 渠道侧请求的 `apiOperation`、路由码 / 子商户 ID 正确
- [ ] 无 5xx、无超时、无重试堆叠

## ③ 数据库落库

- [ ] 该落库的表都有记录(acquireii / tradeii / cmf / payment / reconciliation 等按场景核对),记录数符合预期(不多不少)
- [ ] 该没有记录的表确实没有
- [ ] `status` 状态机流转符合预期
- [ ] 金额字段(`totalAmount` / `dccAmount` / capture amount)数值正确
- [ ] 跨表关联字段一致:`merchantOrderNo` / `paymentSeqNo` / `preauthOrderNo`
- [ ] 跨库一致:`acquireii` ↔ `tradeii` ↔ `cmf`

## ④ Fund Flow(资金流)

- [ ] 该产生入账流水的场景(支付成功 / Capture / Refund):`t_fund_flow` 有对应记录
- [ ] 该没有 Fund Flow 的场景(CREATED 未支付 / 支付失败 / PreAuth 仅冻结 / Void)确认 `t_fund_flow` 确实没有记录 ⭐
- [ ] 借贷平衡:每组分录 Total Dr = Total Cr
- [ ] 方向正确:钱进 → Fund-In ↑ / Merchant ↑;钱出 → Merchant ↓
- [ ] 涉及账户正确:`Fund-In Pending Settlement` / `Merchant Pending for Clearing` / `Merchant Basic` / `Payby Revenue` / `Refund Pending for Clearing`
- [ ] 金额与订单金额、手续费、退款金额对得上

## ⑤ 通知 & 对账

- [ ] `notifyUrl` 收到 POST,body 字段完整(`notify_id` / `notify_timestamp` / 订单对象)
- [ ] 商户回 `{"response":"SUCCESS"}` + HTTP 200 + `application/json` 后不再重试
- [ ] 重试用例:模拟非 SUCCESS / 非 200 / 超时,按 `2 → 10 → 10 → 60 → 120 → 360 → 900` 分钟节奏,第 7 次后停止
- [ ] T+1 对账单 ZIP 下载到,包含本笔(包含 Transaction / Settlement / Fund Statement 三类 CSV;PreAuth 除外,仅 Capture 进对账单)
- [ ] CSV 中 `transactionType` / `status` / `direction` / 金额正确;Revoke 显示为 `REVERTED`
- [ ] Settlement 等式:`totalCredit - totalDebit = settleToBank + stayAmount`

详见 [[merchant-acquisition-notify-and-statement]] / [[merchant-acquisition-notify-statement-spec]]。

## 横切补充:边界与安全覆盖

按 [[merchant-acquisition-test-case-skeleton-abcde]] 的 D / E 组覆盖:

- [ ] 幂等:同 `merchantOrderNo` 重复请求 → `62016 MERCHANT_ORDER_NO_EXIST`
- [ ] 跨日:23:59 创建、0:01 通知,归属正确
- [ ] 并发:同单高并发下单
- [ ] 签名异常 / `Partner-Id` 错误 → `403 UNAUTHORIZED`
- [ ] 时间戳超 ±15 分钟 → `400 REQUESTTIME_TOO_EARLY/LATER`
- [ ] 权限:未开通产品包 → `62026 PRODUCT_IS_NOT_APPLIED`
- [ ] 跨商户使用 `cardToken` / `preauthOrderNo` → `Invalid partner id`

## PreAuth 专项提醒 ⭐

PreAuth 用例容易踩坑,单独再过一遍:

- [ ] MPGS 请求是 `AUTHORIZE` 不是 `PAY`
- [ ] `t_preauth_control` 表有记录
- [ ] **没有** Fund Flow(确认 `t_fund_flow` 查不到是预期)
- [ ] **不进** 对账单(Capture 后才进)
- [ ] Void 后不再有 Fund Flow;Capture 后才有入账分录

## 相关参考

- 用例分组(A/B/C/D/E):[[merchant-acquisition-test-case-skeleton-abcde]]
- 测试数据/卡号/金额/`merchantOrderNo` 命名:[[merchant-acquisition-test-data-conventions]] / [[merchant-acquisition-test-data-preparation]]
- 环境域名 / MID / 数据库入口:[[merchant-acquisition-test-environment-and-tools]] / [[merchant-acquisition-test-environment-tools]]
- 调用骨架与签名 Header:[[merchant-acquisition-curl-postman-skeleton]] / [[merchant-acquisition-curl-postman-templates]]
- 方法论总览:[[merchant-acquisition-test-methodology-overview]]
