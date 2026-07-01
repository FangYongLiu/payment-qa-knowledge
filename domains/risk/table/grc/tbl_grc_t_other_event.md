---
id: tbl_grc_t_other_event
object_type: Table
name: GRC其他事件表(grc.t_other_event_<yyyy>)
aliases:
- grc.t_other_event_<yyyy>
- t_other_event
domain: risk
status: active
owner: xinwei.cao,dewen.li
reviewer: xinwei.cao,dewen.li
last_reviewed_at: '2026-06-25'
source_type: wiki
source_ref: confluence:AQ/2161541121
tags:
- grc
- mongodb
- event-store
- yearly-partition
related_services:
- svc_grc_component_connect_provider
related_scenarios:
- scn_grc_event_routing_by_type
- scn_grc_ip_path_engagement_signature
---

# GRC其他事件表(grc.t_other_event_<yyyy>)

## 用途
GRC 风控引擎对非 `PAYMENT` 类事件的持久化集合(MongoDB `grc` 库),按年份分表(`grc.t_other_event_<yyyy>`)。承接 [[svc_grc_component_connect_provider]] 在 `verifyRisk` 请求处理中产生的事件文档落库。

收纳的事件类型(按事件路由规则):`ENTER_WALLET`、`CASHDESK_INIT`、identity 类事件。`PAYMENT` 类事件不落入本表,落入 [[tbl_grc_t_payment_event]]。

## 关联关系
- **所属服务**:[[svc_grc_component_connect_provider]](= frontmatter `related_services`)
- **谁读写它**:GRC 组件在规则执行后写入;Kibana / MongoDB 查询用于 QA 校验。
- **哪些场景校验它**:[[scn_grc_event_routing_by_type]]、[[scn_grc_ip_path_engagement_signature]](= `related_scenarios`)。

## 关键列
事件文档与 `t_payment_event_<yyyy>` 同构:
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `riskStatus` | - | 规则引擎判定后的风控状态 |
| `remoteIpInfo` | object | 解析 `X-Forwarded-For` 后写入的远端 IP 归属信息 |
| `remoteIpInfo._id` | - | IP 解析路径识别签名(path engagement signature);判定 legacy `Ip2location` vs MaxMind GeoIP MMDB |
| `trueIpInfo` | object | 真实 IP 归属信息 |
| action outcome | - | 命中规则后的动作结果 |

## 主键/索引
原文未列出。按年份分表命名规则为 `t_other_event_<yyyy>`(如 `t_other_event_2024`、`t_other_event_2025`)。分表开关同 [[tbl_grc_t_payment_event]](`mongodb.sharding.*`)。

## 校验点(QA 关注)
- **事件路由正确性**:`ENTER_WALLET` / `CASHDESK_INIT` / identity 类事件必须落入 `t_other_event_<yyyy>`,不应错落入 `t_payment_event_<yyyy>`;反之 `PAYMENT` 不应进入本表。
- **按年份分表**:跨年场景确认事件写入到当前年份对应 `<yyyy>` 集合。
- **IP 路径判定以文档为准**:通过 `remoteIpInfo._id` 形态判断 GeoIP 新路径是否生效;不要依赖 `GeoIPOperaUtil` 日志,见 [[scn_grc_geoip_log_not_reliable]]。
- **字段完整性**:`riskStatus`、`remoteIpInfo`、`trueIpInfo` 以及 action outcome 应齐备。
