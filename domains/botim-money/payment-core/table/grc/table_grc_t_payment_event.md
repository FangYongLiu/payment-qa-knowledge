---
id: tbl_grc_t_payment_event
object_type: Table
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-22'
source_type: consolidation
source_ref: consolidation:risk-control:b4
tags:
- grc
- mongodb
- event-store
subdomain: event-persistence
module: null
sensitivity: normal
name: GRC支付事件表 t_payment_event_<yyyy>
aliases:
- t_payment_event
- grc.t_payment_event_<yyyy>
related_services:
- svc_payment
---

## 用途

存储 GRC 风控系统中 `event type = PAYMENT` 的事件文档，位于 MongoDB `grc` 库，按年份分表（`grc.t_payment_event_<yyyy>`）。由 `gp079_grc-component-connect-provider` 在处理 verifyRisk 请求时写入，承载该笔支付事件的风控判定结果与上下文，供后续查询、回溯与路径识别使用。

与之并列的还有 `grc.t_other_event_<yyyy>`，用于承接 `ENTER_WALLET`、`CASHDESK_INIT`、identity 类等非 PAYMENT 事件。事件按类型路由到对应集合，详见 [[scn_grc_event_routing_by_type]]。

## 关键列

- `riskStatus`：风控判定状态。
- `remoteIpInfo`：远端 IP 解析结果。其 `_id` 形态是判定本次请求走 legacy `Ip2location` 还是新 MaxMind GeoIP MMDB 路径的 path engagement signature（见 [[scn_grc_ip_path_engagement_signature]]）。
- `trueIpInfo`：真实 IP 解析结果。
- 命中规则后的 action outcome（规则触发结果字段）。

## 主键/索引

原文未明确给出主键与索引定义。仅说明集合按年份切分（`<yyyy>` 后缀），事件文档以上述关键字段承载状态与解析结果。

## 校验点(QA 关注)

- **事件路由正确性**：`PAYMENT` 事件必须落入 `t_payment_event_<yyyy>`，不能错落到 `t_other_event_<yyyy>`。
- **年份分表落点**：按事件发生时间核对落到对应年份的集合。
- **IP 路径识别**：以事件文档中 `remoteIpInfo._id` 形态作为判定新旧 IP 解析路径（legacy `Ip2location` vs MaxMind GeoIP MMDB / PAYM-2744）的可靠依据，不要依赖 `GeoIPOperaUtil` 日志——该日志仅在出错时打印，不能确认路径是否生效（见 [[scn_grc_geoip_log_not_reliable]]）。
- **riskStatus 与 action outcome 一致性**：核对命中的规则与文档中记录的 action outcome、`riskStatus` 是否一致。
- **`remoteIpInfo` / `trueIpInfo` 完整性**：verifyRisk 请求经 `X-Forwarded-For` 解析后这两个字段应被正确写入。
- **配置变更后的验证时机**：Apollo YAML 类（含 Kill Switch）改动需 Tomcat 重启后再来本表验证；`aml.t_system_param` 改动需走缓存清理流程后再验证事件文档变化，不要立即下结论。
