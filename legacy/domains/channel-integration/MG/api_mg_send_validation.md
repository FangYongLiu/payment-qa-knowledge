---
id: api_mg_send_validation
object_type: API
domain: channel-integration
status: archived
owner: wiki-sync@acquire
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-20'
source_type: wiki
source_ref: confluence:AQ/1268547712
tags:
- MG
- 预校验
- 下单前
subdomain: MG
module: order-processing
sensitivity: normal
name: MG下单预校验接口 (SendValidation)
aliases:
- Pre-Validation
related_services: []
related_tables: []
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
在下单前，对交易请求进行预校验（金额、字段、合规性等）。校验不通过时直接阻断交易，返回具体错误，避免无效订单进入提交流程。

## 路径/方法
原文未提供具体 HTTP 路径与方法。属于 MG（间接渠道）下单流程中的预校验接口（Pre-Validation / SendValidation）。

## 入参
原文未明确列出字段。入参为交易请求相关信息，包括但不限于：
- 金额相关字段
- 收款国家 + 币种下通过 [[api_mg_gffp]] 收集到的所有汇款字段
- 合规性相关字段

## 出参
原文未明确列出字段。返回校验结果：
- 通过：可继续进入下单（[[api_mg_commit]]）流程
- 不通过：返回具体错误信息，阻断交易

## 错误码
原文未给出 SendValidation 接口具体错误码列表。

## 测试校验点
- 调用时机：用户在 Transfer Details 页面点击 Confirm 时触发一次 SendValidation。
- 校验不通过场景：确认前端对返回的具体错误进行展示，且交易被阻断，不进入 commit 流程。
- 校验通过场景：可继续后续支付与 commit 下单流程。
- 字段一致性：传入字段应与 GFFP 返回并在 Transfer Details 页面收集到的字段保持一致。
- 与 FeeLookup 的金额/汇率结果联动校验，确保金额、币种与路由结果一致。
- 超时处理：遵循 MG 渠道整体规则——超时按完全相同参数再次请求（幂等逻辑）。
