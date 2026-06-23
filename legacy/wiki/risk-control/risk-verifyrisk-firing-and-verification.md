---
title: verifyRisk 事件触发与验证方法
domain: risk-control
kind: wiki_page
slug: risk-verifyrisk-firing-and-verification
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki
source_ref: wiki:00c6a300-c75b-4c5d-b0c9-c18e010dfb50
tags: []
---

# verifyRisk 事件触发与验证方法

本页聚焦 Day 4 风控规则触发与验证环节：如何调用 `verifyRisk`、如何用 SGS→CGS 链路覆盖 PAYMENT 事件、如何在 DB/Kibana 中验证命中结果，以及 Kill Switch 与回滚的安全操作。

## verifyRisk 调用方式

- **接口入口**：`https://uat-api-intra.test2pay.com/newriskverify`
- **请求体**：`verifyRisk` 请求，`eventBody` 内携带规则 conditions/columns 用到的字段
- **字段名严格匹配**：payload 字段名必须与 list repo 列字段名完全一致（大小写敏感，无自动映射）
- **关键 Header**：
  - `eventId` → 落入审计备注 `'from visual rule, eventId=<id>'`（取自 Header，**不**取自 body）
  - `X-Forwarded-For` → 用于 IP-area 解析
- **api-forge 工具**：`sim-api-forge.corp.test2pay.com/test/cgs`，环境下拉支持 UAT
- 详见 [[api_grc_verify_risk]]

## E2E PAYMENT 事件触发链路

覆盖真实 PAYMENT 事件的完整调用链（PAYM-2744 TC-23 cashdesk E2E 配方）：

1. SGS `acquire2/placeOrder`
2. CGS `cashdesk/unityInitPayPage`
3. CGS `cashdesk/confirmPayInfo`

至少需要：

- 一次命中规则 checkpoint 的事件（正向）
- 一次不匹配规则的事件（负向）

## 命中验证：列表库与事件文档

- **查 list repo 写入**：
  ```
  db.bigdata_list_repo_data.find({repoNo:'<target>'}).sort({_id:-1}).limit(3)
  ```
- **查事件文档**：在 `t_payment_event_<yyyy>` / `t_other_event_<yyyy>` 中确认
  - `riskStatus`
  - `remoteIpInfo`、`trueIpInfo`
  - action 执行结果
- **审计备注格式**：`'from visual rule, eventId=<id>'`
- **空值语义**：
  - `oneRow`：仅静默跳过空白 attr
  - `mostRow`：整行写入终止
- **异常处理预期**：
  - 非法 `repoNo`（被篡改的 POST）应被 `addListRepos` 字典拒绝
  - 目标 list repo 已被热删除 → 优雅 no-op + 日志，不抛异常

## 缓存刷新（systemParam + ip）

运行时开关 `aml.t_system_param` 改动后，**仅在 Risk Param 页 Save 不足以生效**，必须执行：

- Basis → Function Query → Cache Clear → `gp079_grc-component-connect-provider` → `systemParam` Clear + `ip` Clear

## Kibana 日志检索

- 通过 `eventId` / `cisTicket` / `orderNo` 定位 GRC service 日志
- `GeoIPOperaUtil` **仅在 error 时打日志**；判断路径是否走 GeoIP/legacy 主要靠 `remoteIpInfo._id` 文档形态特征（path engagement signature）
- 相关架构与 IP 解析背景见 [[risk-system-architecture-overview]]

## Kill Switch 与回滚

- **Kill Switch（Apollo YAML 类）**：需要 **Tomcat 重启**，非热加载；验证应在重启之后而非立即
- **Trial-mode 规则**：仅写日志、**不执行 action**；通过"list repo 无对应行"反向确认
- **回滚路径（按 blast radius 排序）**：
  1. Visual Rule UI 直接 disable 规则
  2. 翻转 `aml.t_system_param` flag + 执行缓存清除
- 在 sandbox 规则上演练两条 kill 路径（DRAFT 阶段规则可用）

## 相关文档

- 激活流程前置：[[risk-visual-rule-activation-workflow]]
- 规则编写：[[risk-visual-rule-authoring-guide]]
- 策略-检查点-规则层级：[[risk-visual-rule-hierarchy]]
- 后台入口：[[auto_basis_visual_rule_admin]]
