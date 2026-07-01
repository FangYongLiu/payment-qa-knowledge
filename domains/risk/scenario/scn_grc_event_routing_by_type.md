---
id: scn_grc_event_routing_by_type
object_type: Scenario
name: 事件按类型路由到对应集合校验
aliases: []
domain: risk
status: active
owner: xinwei.cao,dewen.li
reviewer: xinwei.cao,dewen.li
last_reviewed_at: '2026-06-25'
source_type: wiki
source_ref: confluence:AQ/2161541121
tags:
- GRC
- event-routing
- MongoDB
related_services:
- svc_grc_component_connect_provider
related_tables:
- tbl_grc_t_payment_event
- tbl_grc_t_other_event
---

# 事件按类型路由到对应集合校验

## 触发/入口
- 通过 [[api_grc_verify_risk]] 进入 GRC 组件 [[svc_grc_component_connect_provider]],触发不同 event type 的风控请求。

## 关联关系
- **涉及服务**:[[svc_grc_component_connect_provider]](= `related_services`)
- **校验的表**:[[tbl_grc_t_payment_event]]、[[tbl_grc_t_other_event]](= `related_tables`)

## 前置条件
- GRC 组件正常运行,可读写 MongoDB `grc` 库。
- 覆盖事件类型:`PAYMENT`、`ENTER_WALLET`、`CASHDESK_INIT`、identity 类事件。
- 明确当前年份 `<yyyy>`,用于定位年份分表。

## 操作步骤
1. 分别构造并发送 `PAYMENT` / `ENTER_WALLET` / `CASHDESK_INIT` / identity 类 verifyRisk 请求。
2. 等待 GRC 组件完成规则执行与事件落库。
3. 在 MongoDB `grc` 库中按事件类型对应的年份分表集合查询事件文档。

## DB 校验点
- `PAYMENT` 事件 → `grc.t_payment_event_<yyyy>`。
- `ENTER_WALLET` / `CASHDESK_INIT` / identity 类事件 → `grc.t_other_event_<yyyy>`。
- 事件文档应含:`riskStatus`、`remoteIpInfo`、`trueIpInfo`、action outcome。

## 预期结果
- 各类型事件分别且仅写入其对应集合,年份分表后缀 `<yyyy>` 正确。
- `PAYMENT` 不出现在 `t_other_event_<yyyy>`;其它类型不出现在 `t_payment_event_<yyyy>`。
- 事件文档字段结构完整,可用于后续触发与验证(见 [[flow_verify_risk_request]])。
