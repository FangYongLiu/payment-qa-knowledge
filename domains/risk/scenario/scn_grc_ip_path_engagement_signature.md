---
id: scn_grc_ip_path_engagement_signature
object_type: Scenario
name: 通过remoteIpInfo._id判定IP解析路径
aliases: []
domain: risk
status: active
owner: xinwei.cao,dewen.li
reviewer: xinwei.cao,dewen.li
last_reviewed_at: '2026-06-25'
source_type: wiki
source_ref: confluence:AQ/2161541121
tags:
- GeoIP
- Ip2location
- MaxMind
- verifyRisk
related_services:
- svc_grc_component_connect_provider
related_tables:
- tbl_grc_t_payment_event
- tbl_grc_t_other_event
---

# 通过remoteIpInfo._id判定IP解析路径

## 触发/入口
- verifyRisk 请求通过 Header `X-Forwarded-For` 携带 IP,到达 [[svc_grc_component_connect_provider]] 后由 GRC 解析 IP 归属地。
- 解析存在两条路径:旧路径 `Ip2location`(legacy);新路径 MaxMind GeoIP MMDB(PAYM-2744 IP-Location Optimization)。

## 关联关系
- **涉及服务**:[[svc_grc_component_connect_provider]](= `related_services`)
- **校验的表**:[[tbl_grc_t_payment_event]]、[[tbl_grc_t_other_event]](= `related_tables`)
- **相关场景**:[[scn_grc_geoip_log_not_reliable]]

## 前置条件
- verifyRisk 请求已落库,对应事件文档已写入 `grc.t_payment_event_<yyyy>` 或 `grc.t_other_event_<yyyy>`。
- 事件文档包含 `remoteIpInfo` 字段。

## 操作步骤
1. 根据 event type 定位事件集合(`PAYMENT` → payment_event;其他 → other_event)。
2. 查询目标事件文档,取出 `remoteIpInfo._id` 字段。
3. 依据 `remoteIpInfo._id` 形态判定本次请求实际走的是 MaxMind GeoIP 还是 legacy `Ip2location`。
4. 不要以 `GeoIPOperaUtil` 日志为判定依据——该工具仅在出错时打日志,无日志不代表新路径未生效。

## DB 校验点
- 集合:`grc.t_payment_event_<yyyy>` / `grc.t_other_event_<yyyy>`
- 字段:`remoteIpInfo._id`(路径签名)、`remoteIpInfo`、`trueIpInfo`

## 预期结果
- 通过 `remoteIpInfo._id` 形态可稳定区分本次 verifyRisk 走的是 MaxMind GeoIP 新路径还是 legacy `Ip2location` 旧路径。
- 这是判定新旧 IP 解析引擎是否实际生效的可靠手段(path engagement signature),优先于日志判断。
