---
id: flow_verify_risk_request
object_type: Flow
domain: risk-control
status: archived
owner: consolidation
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-22'
source_type: consolidation
source_ref: consolidation:risk-control:b4
tags:
- GRC
- verifyRisk
- 风控
subdomain: null
module: null
sensitivity: normal
name: verifyRisk请求处理端到端链路
aliases: []
related_services:
- svc_grc_component_connect_provider
related_tables:
- tbl_grc_t_payment_event
- tbl_grc_t_other_event
- tbl_aml_t_system_param
related_scenarios:
- scn_grc_ip_path_engagement_signature
- scn_grc_event_routing_by_type
- scn_grc_geoip_log_not_reliable
related_logs: []
related_requirements: []
related_failures: []
---

## 概述

verifyRisk 请求从 API 入口进入 GRC 核心组件 `gp079_grc-component-connect-provider`(见 [[svc_grc_component_connect_provider]])，经 `X-Forwarded-For` Header 解析 IP 归属地，按事件类型命中策略/Checkpoint 执行规则，最终事件文档落库到对应 MongoDB 集合(按年份分表)，附带 `riskStatus` 与命中规则的 action outcome。

## 步骤(跨系统)

1. **API 入口**：请求经 `verifyRisk` API 进入 GRC 组件 `gp079_grc-component-connect-provider`。
2. **IP 解析**：解析 Header `X-Forwarded-For` 携带的 IP，走以下两条路径之一：
   - 旧路径 `Ip2location`(legacy)
   - 新路径 MaxMind GeoIP MMDB(PAYM-2744 IP-Location Optimization)
   
   解析结果写入事件文档的 `remoteIpInfo` / `trueIpInfo` 字段。路径识别依据 `remoteIpInfo._id` 形态签名(参见 [[scn_grc_ip_path_engagement_signature]])。
3. **规则执行**：按 event type 命中策略 / Checkpoint，执行规则引擎。
4. **事件落库**：事件文档按类型路由到对应 MongoDB 集合(参见 [[scn_grc_event_routing_by_type]])：
   - `PAYMENT` → `grc.t_payment_event_<yyyy>`([[tbl_grc_t_payment_event]])
   - `ENTER_WALLET` / `CASHDESK_INIT` / identity 类 → `grc.t_other_event_<yyyy>`([[tbl_grc_t_other_event]])
   
   文档关键字段：`riskStatus`、`remoteIpInfo`、`trueIpInfo` 及 action outcome。

## 涉及服务/表

- 服务：[[svc_grc_component_connect_provider]] (`gp079_grc-component-connect-provider`)
- 持久化集合：
  - [[tbl_grc_t_payment_event]] `grc.t_payment_event_<yyyy>`
  - [[tbl_grc_t_other_event]] `grc.t_other_event_<yyyy>`
- 运行时配置：[[tbl_aml_t_system_param]] `aml.t_system_param`
- 管理面 / 观测：Basis Admin、AstraShield、Kibana、MongoDB(`grc` / `aml` / `bigdata` 库)

## 校验点

- **IP 解析路径判定**：以事件文档 `remoteIpInfo._id` 形态签名为准，不能依赖 `GeoIPOperaUtil` 日志(该工具仅在出错时打日志，参见 [[scn_grc_geoip_log_not_reliable]])。
- **事件路由正确性**：根据事件类型核对落库集合是 `t_payment_event_<yyyy>` 还是 `t_other_event_<yyyy>`。
- **事件文档关键字段**：`riskStatus`、`remoteIpInfo`、`trueIpInfo`、action outcome 完整。
- **配置生效路径**：
  - Apollo YAML(含 Kill Switch)为构建/重启时生效，**非热更新**，改完必须等 Tomcat 重启后再验证。
  - `aml.t_system_param` 为运行时生效，须经 Basis → Function Query → Cache Clear → `gp079_grc-component-connect-provider` → `systemParam` Clear(+ `ip` Clear) 流程刷新；仅在 Risk Param 页 Save 不足以生效。
