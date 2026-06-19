---
title: 风控规则触发与验证操作手册
domain: risk-control
kind: wiki_page
slug: risk-rule-firing-and-verification
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:AQ/2161541121
tags: []
---

# 风控规则触发与验证操作手册

本页讲解如何通过 `verifyRisk` 接口触发风控规则、构造 PAYMENT 事件链路，以及如何在 list_repo、event_doc 与 Kibana 中验证规则命中结果。

## 触发入口与契约

- 端点：`https://uat-api-intra.test2pay.com/newriskverify`
- 调用方式：`verifyRisk` 请求，`eventBody` 携带规则 conditions/columns 所引用的字段
- **字段名精确匹配**：payload 字段名必须与规则列名/条件名完全一致（区分大小写，无自动映射）
- 请求头 `eventId` → 写入审计备注 `'from visual rule, eventId=<id>'`（取自 header，**不是** body）
- 请求头 `X-Forwarded-For` → 用于 IP 区域解析
- 工具：api-forge UI `sim-api-forge.corp.test2pay.com/test/cgs`，环境下拉支持 UAT

相关：[[api_grc_verify_risk]]、[[risk-visual-rule-authoring-guide]]

## E2E PAYMENT 事件链路

覆盖 PAYMENT 事件类型时，按以下顺序串接调用：

1. SGS `acquire2/placeOrder`
2. CGS `cashdesk/unityInitPayPage`
3. CGS `cashdesk/confirmPayInfo`

参考：PAYM-2744 TC-23 cashdesk E2E recipe。

## 用例覆盖要求

每条规则上线验证至少需要：

- **正向用例**：构造命中规则 checkpoint 与条件的 `verifyRisk` 事件
- **负向用例**：构造不匹配规则的事件，确认未触发

## list_repo 数据校验

查询目标 list repo 中最新写入的若干行：

```
db.bigdata_list_repo_data.find({repoNo:'<target>'}).sort({_id:-1}).limit(3)
```

校验要点：

- 命中后应能定位到规则写入的行；未命中需能解释缺失原因
- 部分空值语义：`oneRow` 静默跳过空白属性；`mostRow` 整行中止写入
- 篡改 POST 中的未知 `repoNo` 应被 `addListRepos` 字典拒绝
- 目标 list repo 被热删除时应 graceful no-op + 日志记录，而非抛异常
- 审计备注格式固定：`'from visual rule, eventId=<id>'`

list 仓结构与字典定义参考 [[risk-visual-rule-authoring-guide]]。

## event_doc 校验

事件文档落库于 `grc.t_payment_event_<yyyy>` 或 `grc.t_other_event_<yyyy>`，需校验字段：

- `riskStatus`：规则动作执行结果
- `remoteIpInfo`：IP 区域解析结果
- `remoteIpInfo._id`：**路径参与签名**，用于识别走的是 GeoIP MMDB 还是 legacy `Ip2location`
- `trueIpInfo`
- 规则的 action outcome（如 `ADD_TO_LIST` 是否实际写入）

注意：Trial 模式下规则只写日志、**不执行 action**——通过 list_repo 行的缺失来验证。

## Kibana 日志查询

- 业务域：`domain=risk-control`（GRC 服务日志）
- 常用检索键：`eventId`、`cisTicket`、`orderNo`
- `GeoIPOperaUtil` 仅在出错时打日志；判断路径走向需依赖 `remoteIpInfo` 文档形态签名而非日志

## 排错快速通道

事件未按预期命中时，依次自查：规则状态 / checkpoint 是否匹配 / Strategy 版本是否为 deployed / 缓存是否过期 / 字段名拼写是否一致。

详见 [[risk-troubleshooting-checklist]]；缓存层面操作见 [[risk-cache-clear-and-killswitch]]；规则上线流程见 [[risk-visual-rule-activation-workflow]]。
