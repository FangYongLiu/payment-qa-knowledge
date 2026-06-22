---
id: scn_grc_event_routing_by_type
object_type: Scenario
domain: risk-control
status: active
owner: consolidation
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-22'
source_type: consolidation
source_ref: consolidation:risk-control:b4
tags:
- GRC
- event-routing
- MongoDB
subdomain: grc
module: event-persistence
sensitivity: normal
name: 事件按类型路由到对应集合校验
aliases: []
related_services:
- svc_grc_component_connect_provider
related_tables:
- tbl_grc_t_payment_event
- tbl_grc_t_other_event
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 触发/入口
- 通过 `verifyRisk` API 进入 GRC 组件 `gp079_grc-component-connect-provider`，触发不同 event type 的风控请求。

## 前置条件
- GRC 组件正常运行，可读写 MongoDB `grc` 库。
- 测试覆盖以下事件类型：`PAYMENT`、`ENTER_WALLET`、`CASHDESK_INIT`、identity 类事件。
- 明确当前年份 `<yyyy>`，用于定位年份分表。

## 操作步骤
1. 分别构造并发送以下事件类型的 verifyRisk 请求：
   - `PAYMENT` 类事件
   - `ENTER_WALLET` 类事件
   - `CASHDESK_INIT` 类事件
   - identity 类事件
2. 等待 GRC 组件完成规则执行与事件落库。
3. 在 MongoDB `grc` 库中按事件类型对应的年份分表集合查询事件文档。

## DB 校验点
- `PAYMENT` 事件 → 落入 `grc.t_payment_event_<yyyy>`。
- `ENTER_WALLET` 事件 → 落入 `grc.t_other_event_<yyyy>`。
- `CASHDESK_INIT` 事件 → 落入 `grc.t_other_event_<yyyy>`。
- identity 类事件 → 落入 `grc.t_other_event_<yyyy>`。
- 事件文档中应包含关键字段：`riskStatus`、`remoteIpInfo`、`trueIpInfo`，以及命中规则后的 action outcome。

## 预期结果
- 各类型事件分别且仅写入其对应的目标集合，年份分表后缀 `<yyyy>` 正确。
- `PAYMENT` 事件不会出现在 `t_other_event_<yyyy>`；`ENTER_WALLET` / `CASHDESK_INIT` / identity 事件不会出现在 `t_payment_event_<yyyy>`。
- 事件文档字段结构完整，含 `riskStatus` 与 action outcome，可用于后续触发与验证（见 [[flow_verify_risk_request]]）。
