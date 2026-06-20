---
id: api_mg_commit
object_type: API
domain: channel-integration
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-20'
source_type: wiki
source_ref: confluence:AQ/1268547712
tags:
- MG
- 下单
- 订单处理
subdomain: mg
module: order
sensitivity: normal
name: MG下单接口 (commit)
aliases:
- commit
related_services: []
related_tables: []
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
提交最终的汇款订单到MG渠道。成功返回后，系统进入结算流程；下单成功后推送入款的入账流水。

## 路径/方法
原文未提供具体路径与方法。

## 入参
原文未提供具体入参字段。

## 出参
原文未提供具体出参字段。说明：成功返回后系统进入结算流程，并推送入款的入账流水。

## 错误码
原文未列出本接口具体错误码。

通用异常与限制：
- 超时：MG要求请求超时后按完全相同参数再次请求，接口有幂等逻辑。

## 测试校验点
- 调用时机：支付完成后，由 Remittance 通知渠道下单时调用。
- 成功路径：下单成功后系统进入结算流程，并推送入款的入账流水（funding flow）。
- 幂等性：超时场景使用完全相同参数重发，应保证幂等，不产生重复订单。
- 状态联动：下单提交后订单进入 CRS (CHANNEL_REMITTANCE_SUBMITED) → MG state=AVAIL，需配合 [[api_mg_order_status_query]] 持续轮询同步后续状态。
- 前置依赖：依赖 [[api_mg_send_validation]] 预校验通过后才会进入下单流程。
- 失败处理：若后续查询返回失败状态，由 Remittance 触发退款逻辑（参见 [[api_mg_send_reversal]]）。
