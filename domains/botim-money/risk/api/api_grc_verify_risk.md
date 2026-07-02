---
id: api_grc_verify_risk
object_type: API
name: verifyRisk 风控校验接口
aliases:
- verifyRisk
- newriskverify
domain: risk
status: active
owner: xinwei.cao,dewen.li
reviewer: xinwei.cao,dewen.li
last_reviewed_at: '2026-06-25'
source_type: wiki
source_ref: confluence:AQ/2161541121
tags:
- verifyRisk
- GRC
- newriskverify
- risk-engine
related_services:
- svc_grc_component_connect_provider
related_tables:
- tbl_grc_t_payment_event
- tbl_grc_t_other_event
related_scenarios:
- scn_grc_event_routing_by_type
- scn_grc_ip_path_engagement_signature
---

# verifyRisk 风控校验接口

## 用途
向 GRC 风控引擎提交一次风控校验请求,触发 Visual Rule 的 Strategy → Checkpoint → Rule 链路评估,并按命中规则执行 action(`ADD_TO_LIST` / `REJECT` / `REVIEW` / `PASS` / value-set actions),同时将事件文档持久化到对应事件集合([[tbl_grc_t_payment_event]] 或 [[tbl_grc_t_other_event]])。承载服务为 [[svc_grc_component_connect_provider]]。

## 路径/方法
- UAT Endpoint:`https://uat-api-intra.test2pay.com/newriskverify`
- 接口名:`verifyRisk`,HTTP 请求承载 `verifyRisk` 请求体。
- 触发工具:api-forge UI `sim-api-forge.corp.test2pay.com/test/cgs`(环境下拉支持 UAT)。
- 端到端 PAYMENT 事件触发链路(替代直调,PAYM-2744 TC-23 cashdesk E2E 配方):SGS `acquire2/placeOrder` → CGS `cashdesk/unityInitPayPage` → CGS `cashdesk/confirmPayInfo`。

## 入参
- **Body**:`verifyRisk` 请求,核心为 `eventBody`,承载规则条件/列所引用的事件字段。
  - **字段名精确匹配契约**:payload 字段名必须与列 `field` 名完全一致(大小写敏感,无自动映射)。字段名错配是规则不命中/写入失败的常见原因。
- **Header**:
  - `eventId`:命中后写入审计备注,格式 `'from visual rule, eventId=<id>'`。**取自请求 Header,不是 body**。
  - `X-Forwarded-For`:用于 IP-area 解析(MaxMind GeoIP MMDB / legacy `Ip2location`)。
- 事件类型:`PAYMENT`、`ENTER_WALLET`、`CASHDESK_INIT`、identity events 等。

## 出参
原文未给出响应字段结构。可观测副作用:
- 事件文档落库:`PAYMENT` → `grc.t_payment_event_<yyyy>`([[tbl_grc_t_payment_event]]);其他 → `grc.t_other_event_<yyyy>`([[tbl_grc_t_other_event]])。文档含 `riskStatus`、`remoteIpInfo`(含路径签名 `remoteIpInfo._id`)、`trueIpInfo`、action outcome。
- 命中 `ADD_TO_LIST` 时:目标 list repo(`bigdata_list_repo_data`)写入对应 `repoNo` 行;审计备注 `'from visual rule, eventId=<id>'`。

## 错误码
原文未列出错误码枚举,仅描述行为约定:
- 未知/被篡改的 `repoNo`(不在 `bigdata_system_dic.addListRepos` 字典内)→ 拒绝。
- 目标 list repo 被热删除 → graceful no-op + 一行日志,**不**抛异常。
- `oneRow` 部分字段为空 → 静默跳过该空 attr;`mostRow` 任一字段为空 → 整行写入中止。
- Trial 模式规则 → 仅写日志,不执行 action(list repo 无对应行);rule-level 与 strategy-level 短路各自独立。

## 测试校验点
被以下场景测:[[scn_grc_event_routing_by_type]]、[[scn_grc_ip_path_engagement_signature]]、[[scn_grc_geoip_log_not_reliable]]、[[scn_grc_config_effectiveness]];排障见 [[ts_risk_rule_not_firing]]。
- **正向**:构造命中规则 checkpoint 与条件的事件,校验:
  - list repo 写入:`db.bigdata_list_repo_data.find({repoNo:'<target>'}).sort({_id:-1}).limit(3)`
  - 事件文档:`riskStatus`、`remoteIpInfo`、`trueIpInfo`、action outcome
  - 审计备注:`'from visual rule, eventId=<id>'`,且 `eventId` 来自请求 Header
- **负向**:构造不命中事件,确认 list repo 无写入、事件文档仍正常落库、`riskStatus` 符合预期。
- **字段契约**:故意大小写错配/换名 → 规则不命中(验证无自动映射)。
- **Header 契约**:缺失/错误 `eventId` → 审计备注无法回写正确 id;`X-Forwarded-For` 变更 → `remoteIpInfo` 解析变化。
- **路径签名**:通过 `remoteIpInfo._id` 形态判断走 GeoIP MMDB 还是 legacy `Ip2location`(`GeoIPOperaUtil` 仅在出错时打日志,需依赖文档形态)。
- **Trial 模式短路**:trial 状态 verifyRisk 不应触发动作(仅日志),通过 list repo 行缺失反证。
- **缓存语义**:规则启用后约 35s 缓存重载;运行时参数改动须走 Cache Clear(`systemParam` + `ip`)。
- **Kibana 日志**:用 `eventId` / `cisTicket` / `orderNo` 定位 GRC 服务日志。
