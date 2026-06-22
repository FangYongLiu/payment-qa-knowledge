---
id: svc_grc_component_connect_provider
object_type: Service
domain: risk-control
status: active
owner: consolidation
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-22'
source_type: consolidation
source_ref: consolidation:risk-control:b4
tags:
- risk-control
- grc
- rule-engine
subdomain: grc
module: null
sensitivity: normal
name: GRC风控核心组件 gp079_grc-component-connect-provider
aliases:
- gp079_grc-component-connect-provider
- GRC 组件
related_services: []
related_tables:
- tbl_grc_t_payment_event
- tbl_grc_t_other_event
- tbl_aml_t_system_param
related_scenarios:
- scn_grc_ip_path_engagement_signature
- scn_grc_event_routing_by_type
- scn_grc_apollo_killswitch_restart_required
- scn_grc_system_param_cache_refresh
- scn_grc_geoip_log_not_reliable
- scn_grc_rollback_path_selection
related_logs: []
related_requirements: []
related_failures: []
---

## 职责

- 位于风控请求链路的核心位置，承接 `verifyRisk` API 请求并驱动规则引擎。
- 解析请求 Header `X-Forwarded-For` 携带的 IP，写入事件文档的 `remoteIpInfo` / `trueIpInfo` 字段；存在两条解析路径：
  - 旧路径 `Ip2location`（legacy）
  - 新路径 MaxMind GeoIP MMDB（PAYM-2744 IP-Location Optimization）
  - 路径识别以事件文档中 `remoteIpInfo._id` 的形态为准（path engagement signature）
- 按事件类型命中策略 / Checkpoint 并执行规则，将事件文档落库到对应 MongoDB 集合，附带 `riskStatus` 与 action outcome。

## 上下游依赖

- 上游入口：`verifyRisk` API。
- 管理面 / 周边系统：
  - Basis Admin (`uat.intra.azure.test2pay.com/bigdata-admin/`)
  - AstraShield
  - Kibana
  - MongoDB（读 `grc` / `aml` / `bigdata` 库）
- 配置来源（双开关模型）：
  - **Apollo YAML**：构建期或 Tomcat 重启时加载，Kill Switch 类配置走此路径，**非热更新**，改完必须等重启后再验证。
  - **`aml.t_system_param`**：运行时配置，可通过缓存刷新生效。刷新方式：Basis → Function Query → Cache Clear → `gp079_grc-component-connect-provider` → `systemParam` Clear（+ `ip` Clear）。仅在 Risk Param 页点 Save 不足以生效。

## 涉及 API/表

- API：`verifyRisk`
- MongoDB 集合（按事件类型路由，按年份分表）：

| 事件类型 | 持久化集合 |
|---|---|
| `PAYMENT` | [[tbl_grc_t_payment_event]] `grc.t_payment_event_<yyyy>` |
| `ENTER_WALLET` | [[tbl_grc_t_other_event]] `grc.t_other_event_<yyyy>` |
| `CASHDESK_INIT` | [[tbl_grc_t_other_event]] `grc.t_other_event_<yyyy>` |
| identity 类事件 | [[tbl_grc_t_other_event]] `grc.t_other_event_<yyyy>` |

- 事件文档关键字段：`riskStatus`、`remoteIpInfo`、`trueIpInfo`、命中规则后的 action outcome。
- 运行时参数表：[[tbl_aml_t_system_param]] `aml.t_system_param`。

## 负责人/Owner

- 原文未注明。

## 常见问题

- **Apollo Kill Switch 改完立即验证拿不到新值**：Apollo YAML 非热更新，必须等 Tomcat 重启后再验证，不要立即下结论（见 [[scn_grc_apollo_killswitch_restart_required]]）。
- **`aml.t_system_param` 改完不生效**：仅在 Risk Param 页点 Save 不足，必须走 Basis → Function Query → Cache Clear → `gp079_grc-component-connect-provider` → `systemParam` Clear（+ `ip` Clear）（见 [[scn_grc_system_param_cache_refresh]]）。
- **判断 IP 解析走新/旧路径**：以事件文档中 `remoteIpInfo._id` 形态为准，`GeoIPOperaUtil` 仅在出错时打日志，**不能依赖日志确认路径是否生效**（见 [[scn_grc_ip_path_engagement_signature]]、[[scn_grc_geoip_log_not_reliable]]）。
- **回滚路径选择**：UI 禁用规则 vs 翻转 `aml.t_system_param` 标志位 + 清缓存，按 blast radius 选择（见 [[scn_grc_rollback_path_selection]]）。
