---
title: 风控规则未生效自查清单
domain: risk-control
kind: wiki_page
slug: risk-troubleshooting-checklist
status: archived
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:AQ/2161541121
tags: []
---

# 风控规则未生效自查清单

当一条 Visual Rule 看似配置完成、却没有在事件中触发时，先按本清单逐项排查，能定位绝大多数问题；仍无法定位再升级到对应联系人。

## 常见原因清单

按出现频率从高到低排查：

- **Checkpoint 不匹配**：规则挂载的 checkpoint 与事件实际进入的 checkpoint 不一致；确认 checkpoint 是否绑定到真实 CGS 事件源（而非 test-only）。
- **策略版本未部署**：一个 Strategy 同一时间只有 ONE version 处于 deployed 状态；挂在非 deployed 版本下的规则在真实事件上永远不会 fire。
- **规则状态未到 ENABLED**：仍处于 `DRAFT` 或 `TRIAL`；TRIAL 模式只写日志、不执行 action，rule-level 与 strategy-level 的 trial 短路是独立生效的。
- **缓存陈旧**：审批通过后需等 ~35s 缓存重载；运行时开关 `aml.t_system_param` 改动后必须走 Cache Clear 流程，仅在 "Risk Param page → Save" 是不够的。
- **字段名大小写 / 拼写不一致**：payload 字段必须与 list repo 的 column field name **完全一致**（case-sensitive，无 auto-mapping）。
- **Kill Switch 未生效**：Apollo YAML 类型的 kill switch 不是 hot-reloadable，需 Tomcat 重启后再验证。
- **List repo 列形态选错**：`oneRow` 与 `mostRow` 的列语义不同；`oneRow` 部分留空会静默跳过该 attr，`mostRow` 部分留空会 abort 整行。
- **repoNo 异常**：未在 `bigdata_system_dic.addListRepos` 字典内的 repoNo 会被拒绝；目标 list repo 已被热删除时为 graceful no-op + 一行日志，不会抛异常。

## 自查步骤

按顺序执行：

1. **确认规则状态**：在 Visual Rule UI 检查是否为 `ENABLED`；查 AstraShield 的 Audit Record 确认审批已通过。
2. **确认策略版本**：在 Strategy Manager 查看当前 deployed 的版本号，确认你的规则挂在该版本下。
3. **确认 checkpoint 绑定**：核对 checkpoint 名称（如 `FT_ATL_CP`）以及它对接的事件源。
4. **执行缓存清理**：Basis → Function Query → Cache Clear → `gp079_grc-component-connect-provider` → `systemParam` Clear + `ip` Clear。
5. **核对字段名**：对照 list repo 的 `fieldDef` 列名（`mostRow`）或 `listRepoFieldType`（`oneRow`），逐字段比对 payload 中的 key（含大小写）。
6. **查 Kibana 日志**：用 `eventId` / `cisTicket` / `orderNo` 检索 GRC 服务日志，定位规则是否被命中、是否走 trial 短路。
7. **查 DB 落库**：
   - List repo：`db.bigdata_list_repo_data.find({repoNo:'<target>'}).sort({_id:-1}).limit(3)`
   - 事件文档：在 `t_payment_event_<yyyy>` / `t_other_event_<yyyy>` 查 `riskStatus`、`remoteIpInfo`、`trueIpInfo` 与 action 结果。
8. **核对 Audit memo**：格式应为 `'from visual rule, eventId=<id>'`，其中 `eventId` 取自请求 header，而非 body。

## 路径与签名识别

- 通过事件文档中 `remoteIpInfo._id` 的形态判断走的是 MaxMind GeoIP MMDB 还是 legacy `Ip2location` 路径。
- `GeoIPOperaUtil` 仅在出错时打日志，不能仅靠日志判断路径是否生效，应以 doc-shape 签名为准。

## 升级联系人

排查完仍无法定位时，按问题域升级：

- **Risk Dev（引擎/代码层）**：chao.li@astratech.ae、Abhimanyu.Singh@astratech.ae
- **BMOC（商户配置）**：通过 BMOC Portal 对接业务侧
- **Infra / Ops（缓存、Apollo、VPN、账号）**：zhiqi.jin@astratech.ae
- **QA（用例与验证流程）**：ext_Nitesh.Parasher@astratech.ae

## 相关页面

- 规则生命周期：[[risk-visual-rule-activation-workflow]]
- 触发与验证操作：[[risk-rule-firing-and-verification]]
- 缓存清理与 Kill Switch：[[risk-cache-clear-and-killswitch]]
- 规则编写：[[risk-visual-rule-authoring-guide]]
- 系统总览：[[risk-system-architecture-overview]]
- 接口契约：[[api_grc_verify_risk]]
