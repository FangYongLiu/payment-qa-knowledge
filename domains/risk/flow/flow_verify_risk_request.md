---
id: flow_verify_risk_request
object_type: Flow
name: verifyRisk请求处理端到端链路
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
- verifyRisk
- 风控
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
---

# verifyRisk请求处理端到端链路

## 概述
verifyRisk 请求从 API 入口进入 GRC 核心组件 [[svc_grc_component_connect_provider]](`gp079_grc-component-connect-provider`),经 `X-Forwarded-For` Header 解析 IP 归属地,按事件类型命中策略/Checkpoint 执行规则,最终事件文档落库到对应 MongoDB 集合(按年份分表),附带 `riskStatus` 与命中规则的 action outcome。

## 步骤(跨系统)
1. **API 入口**:请求经 [[api_grc_verify_risk]] 进入 GRC 组件 `gp079_grc-component-connect-provider`。
2. **IP 解析**:解析 Header `X-Forwarded-For` 携带的 IP,走以下两条路径之一:
   - 旧路径 `Ip2location`(legacy)
   - 新路径 MaxMind GeoIP MMDB(PAYM-2744 IP-Location Optimization)
   解析结果写入事件文档 `remoteIpInfo` / `trueIpInfo`;路径识别依据 `remoteIpInfo._id` 形态签名(见 [[scn_grc_ip_path_engagement_signature]])。
3. **规则执行**:按 event type 命中策略/Checkpoint,执行规则引擎。
4. **事件落库**:事件文档按类型路由到对应 MongoDB 集合(见 [[scn_grc_event_routing_by_type]]):
   - `PAYMENT` → [[tbl_grc_t_payment_event]] `grc.t_payment_event_<yyyy>`
   - `ENTER_WALLET` / `CASHDESK_INIT` / identity 类 → [[tbl_grc_t_other_event]] `grc.t_other_event_<yyyy>`
   文档关键字段:`riskStatus`、`remoteIpInfo`、`trueIpInfo` 及 action outcome。

## 关联关系
- **经过的服务(有序)**:[[svc_grc_component_connect_provider]](= `related_services`)
- **关键表**:[[tbl_grc_t_payment_event]]、[[tbl_grc_t_other_event]]、[[tbl_aml_t_system_param]](= `related_tables`)
- **关键场景**:[[scn_grc_ip_path_engagement_signature]]、[[scn_grc_event_routing_by_type]]、[[scn_grc_geoip_log_not_reliable]](= `related_scenarios`)
- **管理面/观测**:Basis Admin([[auto_basis_visual_rule_admin]])、AstraShield、Kibana、MongoDB(`grc` / `aml` / `bigdata` 库)
- **触发接口**:[[api_grc_verify_risk]];排障见 [[ts_risk_rule_not_firing]]

## 校验点
- **IP 解析路径判定**:以事件文档 `remoteIpInfo._id` 形态签名为准,不能依赖 `GeoIPOperaUtil` 日志(仅在出错时打日志,见 [[scn_grc_geoip_log_not_reliable]])。
- **事件路由正确性**:根据事件类型核对落库集合是 `t_payment_event_<yyyy>` 还是 `t_other_event_<yyyy>`。
- **事件文档关键字段**:`riskStatus`、`remoteIpInfo`、`trueIpInfo`、action outcome 完整。
- **配置生效路径**:Apollo YAML(含 Kill Switch)非热更新,改完须等 Tomcat 重启后再验证;`aml.t_system_param`([[tbl_aml_t_system_param]])为运行时生效,须经 Basis → Function Query → Cache Clear → `gp079_grc-component-connect-provider` → `systemParam` Clear(+ `ip` Clear)刷新(见 [[scn_grc_config_effectiveness]])。
