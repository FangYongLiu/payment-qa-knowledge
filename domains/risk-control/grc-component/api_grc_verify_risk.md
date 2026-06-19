---
id: api_grc_verify_risk
object_type: API
domain: risk-control
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-19'
source_type: wiki
source_ref: confluence:AQ/2161541121
tags:
- verifyRisk
- GRC
- risk-engine
subdomain: grc-component
module: connect-provider
sensitivity: normal
name: verifyRisk风控校验接口
aliases: []
related_services: []
related_tables: []
related_scenarios:
- risk-rule-firing-and-verification
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
触发GRC风控校验，将事件送入规则引擎进行Strategy → Checkpoint → Rule链路评估，并按命中规则执行action（如 `ADD_TO_LIST`、`REJECT`、`REVIEW`、`PASS`），同时持久化事件文档到对应event-collection。

## 路径/方法
- Endpoint（UAT）：`https://uat-api-intra.test2pay.com/newriskverify`
- 接口名：`verifyRisk`
- 触发工具：api-forge UI `sim-api-forge.corp.test2pay.com/test/cgs`（env下拉支持UAT）
- 端到端PAYMENT事件链路：SGS `acquire2/placeOrder` → CGS `cashdesk/unityInitPayPage` → CGS `cashdesk/confirmPayInfo`

## 入参
- Body：`verifyRisk` 请求，核心为 `eventBody`，其中字段需对应规则条件/列所引用的事件字段
- 字段名匹配契约：payload字段名必须与列 `field` 名**精确匹配（大小写敏感，无auto-mapping）**
- Header `eventId`：写入审计memo（来源于请求header，**不是**body内字段）
- Header `X-Forwarded-For`：用于IP-area解析（MaxMind GeoIP MMDB / 旧 `Ip2location`）
- 事件类型示例：`PAYMENT`、`ENTER_WALLET`、`CASHDESK_INIT`、identity events

## 出参
- 事件文档落库：
  - `PAYMENT` 类 → `grc.t_payment_event_<yyyy>`
  - 其他 → `grc.t_other_event_<yyyy>`
- 文档关键字段：`riskStatus`、`remoteIpInfo`（含路径签名 `remoteIpInfo._id`）、`trueIpInfo`、action outcome
- 命中 `ADD_TO_LIST` 规则时：`bigdata_list_repo_data` 写入对应 `repoNo` 行
- 审计memo格式：`'from visual rule, eventId=<id>'`（`<id>` 来自请求header `eventId`）

## 错误码
（原文未给出错误码枚举，仅描述以下行为约定）
- 未知 / 被篡改的 `repoNo`（不在 `bigdata_system_dic.addListRepos` 字典内）→ 拒绝
- 目标list repo被hot-deleted → graceful no-op + 日志行（非异常）
- `oneRow` 部分字段为空 → 静默跳过该空attr
- `mostRow` 部分字段为空 → 整行写入中止
- Trial模式规则 → 仅写日志，不执行action（list repo无对应行）

## 测试校验点
- 正向：构造命中规则条件的 `eventBody`，校验：
  1) `bigdata_list_repo_data` 中目标repo出现新行：`db.bigdata_list_repo_data.find({repoNo:'<target>'}).sort({_id:-1}).limit(3)`
  2) event文档中 `riskStatus` / `remoteIpInfo` / `trueIpInfo` / action outcome 正确
  3) 审计memo为 `'from visual rule, eventId=<id>'`，eventId与请求header一致
- 负向：构造不命中事件，确认无list-repo写入且事件doc仍正常落库
- 字段契约：故意大小写错配 → 不应命中（验证无auto-mapping）
- IP路径：通过 `X-Forwarded-For` 注入测试IP，依据 `remoteIpInfo._id` 形态判断走MaxMind GeoIP还是旧 `Ip2location`
- Header来源：审计memo中 `eventId` 必须来自请求header，而非body
- Trial-mode：规则处于TRIAL时仅产生日志，不应有list-repo写入
- 缓存：规则启用后等待~35s缓存reload；必要时执行 Basis → Function Query → Cache Clear → `gp079_grc-component-connect-provider` → `systemParam` Clear + `ip` Clear
- 日志定位：Kibana通过 `eventId` / `cisTicket` / `orderNo` 检索GRC服务日志（注意 `GeoIPOperaUtil` 仅在错误时打日志）
