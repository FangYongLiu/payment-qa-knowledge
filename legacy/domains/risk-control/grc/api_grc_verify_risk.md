---
id: api_grc_verify_risk
object_type: API
domain: risk-control
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-19'
source_type: wiki
source_ref: wiki:00c6a300-c75b-4c5d-b0c9-c18e010dfb50
tags:
- verifyRisk
- GRC
- newriskverify
subdomain: grc
module: null
sensitivity: normal
name: verifyRisk 风控验证接口
aliases: []
related_services: []
related_tables: []
related_scenarios:
- risk-verifyrisk-firing-and-verification
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
向 GRC 风控引擎提交一次风控验证请求，触发 Visual Rule 的检查点（checkpoint）匹配与动作执行（如 `ADD_TO_LIST` / `REJECT` / `REVIEW` / `PASS`），并将事件持久化到事件集合（`grc.t_payment_event_<yyyy>` 或 `grc.t_other_event_<yyyy>`）。

## 路径/方法
- UAT Endpoint: `https://uat-api-intra.test2pay.com/newriskverify`
- 调用方式：HTTP 请求，承载 `verifyRisk` 请求体
- 端到端 PAYMENT 事件触发链路（替代直调）：SGS `acquire2/placeOrder` → CGS `cashdesk/unityInitPayPage` → CGS `cashdesk/confirmPayInfo`
- 调用入口工具：api-forge UI（`sim-api-forge.corp.test2pay.com/test/cgs`，环境下拉支持 UAT）

## 入参
- Body: `verifyRisk` 请求，内含 `eventBody`，承载规则条件 / 列所引用的字段。
  - 字段名严格精确匹配契约：payload 字段名必须与列 `field` 名完全一致（大小写敏感，无自动映射）。
- Header:
  - `eventId`：用于规则命中后写入审计备注，格式为 `'from visual rule, eventId=<id>'`（eventId 取自请求头，**不是** body）。
  - `X-Forwarded-For`：用于 IP 区域解析（IP-area resolver）。

事件类型涵盖：`PAYMENT`、`ENTER_WALLET`、`CASHDESK_INIT`、identity events 等。

## 出参
原文未给出响应字段结构。可观测的副作用：
- 事件文档落库到 `grc.t_payment_event_<yyyy>` 或 `grc.t_other_event_<yyyy>`，包含 `riskStatus`、`remoteIpInfo`、`trueIpInfo` 及动作结果。
- 命中 `ADD_TO_LIST` 规则时，目标 list repo（`bigdata_list_repo_data`）写入对应行；审计备注写入格式 `'from visual rule, eventId=<id>'`。
- IP 路径接入签名可通过 `remoteIpInfo._id` 形状判别（GeoIP MMDB vs 旧版 `Ip2location`）。

## 错误码
原文未直接列出 verifyRisk 的错误码集合。相关异常/拒绝行为：
- 篡改 POST 携带未知 `repoNo`：必须依据 `addListRepos` 字典拒绝。
- 目标 list repo 被热删除：图优雅 no-op + 日志一行，**不**抛异常。
- Trial 模式：仅写一行日志，不执行动作（list-repo 无写入）。
- `oneRow` 部分空值：静默跳过该空 attr；`mostRow` 任一空值：整行 abort。

## 测试校验点
- **正向**：触发一次命中规则 checkpoint 的 `verifyRisk`，校验：
  - list repo 写入：`db.bigdata_list_repo_data.find({repoNo:'<target>'}).sort({_id:-1}).limit(3)`
  - 事件文档：`riskStatus`、`remoteIpInfo`、`trueIpInfo`、动作结果
  - 审计备注：`'from visual rule, eventId=<id>'`，且 `eventId` 来自请求 Header
- **负向**：触发不匹配规则的事件，确认 list repo 无写入、`riskStatus` 与预期一致。
- **字段契约**：故意将 payload 字段名大小写改错或换名 → 规则不命中（验证无自动映射）。
- **Header 契约**：
  - 缺失 / 错误 `eventId` → 审计备注无法回写正确 id。
  - `X-Forwarded-For` 变更 → `remoteIpInfo` 解析变化，验证 IP-area resolver 路径。
- **路径接入签名**：通过 `remoteIpInfo._id` 形状判断走 GeoIP MMDB 还是旧版 `Ip2location`（`GeoIPOperaUtil` 仅在错误时打日志，需依赖 doc 形状）。
- **Kibana 日志检索**：用 `eventId` / `cisTicket` / `orderNo` 定位 GRC 服务日志。
- **缓存语义**：规则启用后约 35s 缓存重载；必要时执行 Basis → Function Query → Cache Clear → `gp079_grc-component-connect-provider` → `systemParam` Clear + `ip` Clear，再次 verifyRisk 复测。
- **Trial 模式短路**：rule-level 与 strategy-level 独立短路，trial 状态下 verifyRisk 不应触发动作（仅日志），通过 list repo 行缺失反证。
- **篡改 / 异常用例**：未知 `repoNo` 必拒；目标 list repo 被删 → no-op + 日志，不抛异常。
