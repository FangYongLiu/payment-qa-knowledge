---
title: 商户收单测试方法论总览
domain: merchant-acquisition
kind: wiki_page
slug: merchant-acquisition-test-methodology-overview
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki
source_ref: wiki:4ef3640b-38b5-4756-81d5-d729c241dc79
tags: []
---

# 商户收单测试方法论总览

商户收单测试不是只测商户接口，而是要验证 **支付中台调用链 + 数据库落库 + 资金流 + 通知 + 对账** 这一整条链路。一笔成功的接口响应只是测试的起点，不是终点。

## 核心理念

- 接口 200 ≠ 测试通过；线上事故复盘表明，"只测前几段不测后几段"是逃逸主因。
- 典型逃逸问题：商户报已付款但订单未支付、对账不平、清算流水缺失。
- 所有场景手册都依赖本页定义的验证骨架、用例分类、命名规范——先读懂本页，再看具体场景。
- 隶属业务域：[[domain_merchant_acquisition]]。

## 五段式 E2E 验证骨架（核心方法论）

所有场景按以下 5 段验证，**缺一不可**。详细展开见 [[merchant-acquisition-e2e-five-stage-verification]]。

| 段 | 验证目标 | 关注点（要点） |
|---|---|---|
| ① 接口响应（API Response） | HTTP/业务码/订单状态 | HTTP 状态码、`head.applyStatus`、`head.code`、`body.acquireOrder.status`、错误码 |
| ② 服务调用链（Service Log） | 链路上每个服务都打到、参数正确 | 每个服务都有日志、关键参数（如 mpgs `apiOperation`）符合预期、无异常/重试堆叠 |
| ③ 数据库落库（DB Persistence） | 表/行数/字段/跨库关联 | 表存在性、记录数量、状态字段、金额字段、跨库关联（acquireii ↔ tradeii ↔ cmf）一致 |
| ④ Fund Flow（资金流） | 会计分录、借贷平衡 | Total Dr = Total Cr、方向正确、涉及 Fund-In Pending / Merchant Pending / Merchant Basic / Payby Revenue |
| ⑤ 通知 & 对账（Notify & Statement） | 异步通知与 T+1 对账 | `notifyUrl` 触发、商户回 `{"response":"SUCCESS"}` 后不再重试、T+1 对账单包含本笔 |

### 关键提醒

- `applyStatus = SUCCESS` ≠ 业务成功，必须看 `code` 与 `status`。
- `CREATED` 是中间态，商户应每 2-6 秒轮询。
- **段 ② 是新 QA 最容易跳过的一段**：traceCode 全链路日志必须每段可查。
- **段 ③ 是商户收单 QA 的"硬功夫"**：每个场景都有"该增加/更新哪些表、各加几条"的明确预期。
- **PreAuth 不进 Fund Flow、不进对账单**——查不到不是 bug，必须 Capture 后才有。

通知重试与对账文件结构详见 [[merchant-acquisition-notify-and-statement]]。

## 标准用例骨架 A/B/C/D/E

每个场景至少覆盖这 5 类用例：

- **A 组 正向流程（Happy Path）**：标准成功、不同卡品牌/支付方式、不同金额段、存卡复用、异步通知+对账。
- **B 组 异常流程（Negative Path）**：参数缺失/非法、内部超时、外部渠道错误（MPGS 特殊 expiry 模拟）、风控拒绝、重复请求/幂等冲突。
- **C 组 数据一致性（Consistency）**：端到端落库、Fund Flow 借贷平衡、跨表关联字段一致、对账单与订单一致。
- **D 组 边界与并发（Boundary & Concurrency）**：金额边界、时间戳边界（±15 分钟）、同 `merchantOrderNo` 并发、跨日订单、长字符串/特殊字符。
- **E 组 权限与安全（Auth & Security）**：未开通产品包（`62026 PRODUCT_IS_NOT_APPLIED`）、跨商户使用资源（`Invalid partner id`）、签名/Partner-Id 错误（`403 UNAUTHORIZED`）、时间戳偏差、IP 白名单。

详细骨架与子项见 [[merchant-acquisition-test-case-skeleton-abcde]]。

## 配套规范与速查

本页只做总览，落地细节分散在以下专题页：

- 环境/域名/账号/MID/工具入口 → [[merchant-acquisition-test-environment-and-tools]]
- `merchantOrderNo` 命名、金额段、测试卡号、特殊 expiry、模拟回调 → [[merchant-acquisition-test-data-conventions]]
- 异步通知重试时间表（2 → 10 → 10 → 60 → 120 → 360 → 900 分钟）与对账单 ZIP/CSV 结构 → [[merchant-acquisition-notify-and-statement]]
- 高频错误码（全局 / 订单状态 / 退款撤销 / 卡片产品 / 风控渠道 / Capture·Void·PreAuth 专属 msg） → [[merchant-acquisition-error-code-quickref]]
- 通用 Header 与 curl/Postman 骨架（PlaceOrder / Refund / Balance / Statement） → [[merchant-acquisition-curl-postman-skeleton]]
- 每跑一笔交易必走的检查清单 → [[merchant-acquisition-per-transaction-checklist]]

## 使用方式

1. 先读本页建立"5 段验证 + ABCDE 用例"心智模型。
2. 按 [[merchant-acquisition-test-environment-and-tools]] 配好环境与账号。
3. 按 [[merchant-acquisition-test-data-conventions]] 准备订单号、金额、卡号。
4. 进入具体场景手册（§5.x：PAYPAGE / DIRECTPAY / PREAUTH 等），按本页 5 段骨架逐项核对。
5. 每笔交易跑完，对照 [[merchant-acquisition-per-transaction-checklist]] 打勾收尾。
