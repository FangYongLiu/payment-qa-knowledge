---
id: scn_grc_geoip_log_not_reliable
object_type: Scenario
domain: risk-control
status: active
owner: consolidation
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-22'
source_type: consolidation
source_ref: consolidation:risk-control:b4
tags:
- geoip
- ip-resolution
- logging
subdomain: ip-area
module: GeoIPOperaUtil
sensitivity: normal
name: GeoIP日志不可作为路径判定依据
aliases: []
related_services:
- svc_grc_component_connect_provider
related_tables:
- tbl_grc_t_payment_event
- tbl_grc_t_other_event
related_scenarios:
- scn_grc_ip_path_engagement_signature
related_logs: []
related_requirements: []
related_failures: []
---

## 触发/入口
verifyRisk 请求经 GRC 组件 `gp079_grc-component-connect-provider` 处理，进入 IP-area 解析阶段。两条解析路径并存：
- 旧路径 `Ip2location`（legacy）
- 新路径 MaxMind GeoIP MMDB（PAYM-2744 IP-Location Optimization）

## 前置条件
- verifyRisk Header `X-Forwarded-For` 携带 IP。
- 期望确认本次请求实际走的是新路径（GeoIP MMDB）还是旧路径（Ip2location）。

## 操作步骤
1. 不要以 `GeoIPOperaUtil` 的日志输出作为路径是否生效的判定依据。
2. 改为查询事件文档（`grc.t_payment_event_<yyyy>` 或 `grc.t_other_event_<yyyy>`），读取 `remoteIpInfo._id` 字段。
3. 通过 `remoteIpInfo._id` 的形态（path engagement signature）判定本次请求所走路径——详见 [[scn_grc_ip_path_engagement_signature]]。

## DB 校验点
- 集合：`grc.t_payment_event_<yyyy>` / `grc.t_other_event_<yyyy>`。
- 字段：`remoteIpInfo._id`（用于识别新旧解析路径）；同时关注 `remoteIpInfo`、`trueIpInfo` 是否被正确写入。

## 预期结果
- `GeoIPOperaUtil` 仅在出错时打印日志，正常路径无日志输出 → 没有日志 ≠ 没走 GeoIP；有/无日志均不能证明路径是否生效。
- 路径判定结论必须以事件文档的结构签名（`remoteIpInfo._id` 形态）为准，而非日志。
