---
id: tbl_grc_t_other_event
object_type: Table
domain: risk-control
status: active
owner: consolidation
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-22'
source_type: consolidation
source_ref: consolidation:risk-control:b4
tags:
- grc
- mongodb
- event-store
- yearly-partition
subdomain: event-persistence
module: grc
sensitivity: normal
name: GRC其他事件表 t_other_event_<yyyy>
aliases:
- grc.t_other_event_<yyyy>
related_services:
- svc_grc_component_connect_provider
related_tables:
- tbl_grc_t_payment_event
related_scenarios:
- scn_grc_event_routing_by_type
- scn_grc_ip_path_engagement_signature
- scn_grc_geoip_log_not_reliable
related_logs: []
related_requirements: []
related_failures: []
---

## 用途

GRC 风控引擎对非 `PAYMENT` 类事件的持久化集合，按年份分表（`grc.t_other_event_<yyyy>`）。承接 `gp079_grc-component-connect-provider` 在 verifyRisk 请求处理中产生的事件文档落库。

收纳的事件类型（按事件路由规则）：

- `ENTER_WALLET`
- `CASHDESK_INIT`
- identity 类事件

`PAYMENT` 类事件不落入本表，落入 [[tbl_grc_t_payment_event]]。

## 关键列

事件文档中关键字段（与 `t_payment_event_<yyyy>` 同构）：

- `riskStatus`：规则引擎判定后的风控状态。
- `remoteIpInfo`：解析 `X-Forwarded-For` 后写入的远端 IP 归属信息。
  - `remoteIpInfo._id`：用作 IP 解析路径识别签名（path engagement signature），通过其形态判定本次请求走的是 legacy `Ip2location` 还是新路径 MaxMind GeoIP MMDB。
- `trueIpInfo`：真实 IP 归属信息。
- action outcome：命中规则后的动作结果。

## 主键/索引

原文未列出。按年份分表的命名规则为 `t_other_event_<yyyy>`（如 `t_other_event_2024`、`t_other_event_2025`）。

## 校验点(QA 关注)

- **事件路由正确性**：`ENTER_WALLET` / `CASHDESK_INIT` / identity 类事件必须落入 `t_other_event_<yyyy>`，不应错落入 `t_payment_event_<yyyy>`；反之 `PAYMENT` 不应进入本表。
- **按年份分表**：跨年场景下需确认事件写入到当前年份对应的 `<yyyy>` 集合。
- **IP 路径判定以文档为准**：通过 `remoteIpInfo._id` 形态判断 GeoIP 新路径是否生效；不要依赖 `GeoIPOperaUtil` 日志（仅出错时打印），日志不可作为路径判定依据。
- **字段完整性**：`riskStatus`、`remoteIpInfo`、`trueIpInfo` 以及 action outcome 应齐备。
- **Kill Switch / 缓存刷新后校验时机**：Apollo YAML 类开关非热更新，需等 Tomcat 重启后再观察本表事件文档以判定规则生效；`aml.t_system_param` 调整后须走 Basis 缓存清理（`systemParam` Clear，必要时叠加 `ip` Clear），再以本表新写入的文档为准验证。
