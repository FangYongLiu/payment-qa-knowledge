---
id: api_mg_fee_lookup
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
- 汇率查询
- 实时汇率
subdomain: MG
module: 汇率查询
sensitivity: normal
name: MG汇率查询接口 (FeeLookup)
aliases:
- FeeLookup
related_services: []
related_tables:
- t_channel_param_mapping
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
查询指定国家币种下支持的所有汇款模式，以及每种模式下的实时汇率。
- 同一模式下可能存在多个 agentid（钱包和 bank 场景会用上，不同钱包要走不同 agentid）
- agentid 提前在 `t_channel_param_mapping` 表里配置，查询时读取该表数据
- 与数据库配置的静态汇率不同，MG 必须实时请求

## 路径/方法
原文未提供具体路径与 HTTP 方法。

## 入参
原文未列出具体入参字段（业务上需传入收款国家、币种等查询条件）。

## 出参
原文提及以下关键返回字段：
- `validCurrencyIndicator`：当 `=false` 时，对应国家要求在最终确认页展示 estimated receive amount 和 estimated exchange rate
- `<ac:totalReceiveFees>`：收款方手续费（如 100），用于在最终确认页展示 Receiver's fee
- `<ac:totalReceiveTaxes>`：收款方税费（如 5），用于在最终确认页展示 Receiver's fee
- 模式列表与对应汇率、agentid 列表

## 错误码
原文未在 FeeLookup 范围内列出具体错误码。

## 测试校验点
- 用户点击 **Send Money**、完成路由后，渠道为 MG 时应触发调用 FeeLookup
- 校验返回的模式与汇率为实时数据，而非数据库静态配置
- 校验同一模式下多个 agentid 的取数逻辑（钱包/bank 场景）正确读取 `t_channel_param_mapping`
- 当 `validCurrencyIndicator=false` 时，最终确认页应展示 estimated receive amount 与 estimated exchange rate
- 当返回包含 `<ac:totalReceiveFees>` / `<ac:totalReceiveTaxes>` 时，最终确认页应展示 Receiver's fee
- 超时场景：按完全相同参数重发请求，需保证幂等
