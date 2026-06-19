---
title: Visual Rule创作指南
domain: risk-control
kind: wiki_page
slug: risk-visual-rule-authoring-guide
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:AQ/2161541121
tags: []
---

# Visual Rule创作指南

本页讲解如何在 Basis Admin 上创作一条 Visual Rule：理解 Strategy → Checkpoint → Rule 三层结构、配置 `ADD_TO_LIST` 动作的两种列模式，以及处理字段精确匹配契约和列表/字典元数据。

## Strategy → Checkpoint → Rule 层级

- **Strategy**：包含 folder、status、effective time，绑定到 Checkpoint。
- **Checkpoint**：触点，例如 `FT Add to list` / `FT_ATL_CP`；需确认是否 wired 到真实 CGS event source，而非 test-only。
- **Rule**：挂在 Strategy 下，由 conditions（事件字段、比较、AND/OR group）+ action 组成。
- 参考已有测试策略 `FT_PAYM2755_TEST`。

### 版本 gotcha
- 一个 Strategy 同时只有 **一个 version 处于 deployed 状态**。
- 挂在 non-deployed version 下的 rule 永远不会在真实事件上 fire。
- 创作时要能识别多版本策略中 deployed 的那一版。

## Visual Rule 区别于其它规则类型

Basis 上同时存在 Visual Rules、Group Rules、Strategy Set，本页仅覆盖 Visual Rules。Action 类型包括 `ADD_TO_LIST`、`REJECT`、`REVIEW`、`PASS` 以及 value-set actions 等。

## ADD_TO_LIST 动作与列模式

`ADD_TO_LIST` 把命中事件写入目标 list repo，写入形态由该 list repo 的 `listRepoAttr` 决定。

### oneRow
- 单一 `[type, value]` 对。
- 字段下拉由 `listRepoFieldType` 过滤。
- **partial-blank 语义**：若某 attr 为空，**静默跳过该 attr**，不影响整条记录写入。

### mostRow
- 多列 row，列由 `fieldDef` 定义，最多 **3 列上限**。
- 字段下拉由 `fieldDef` 列过滤。
- **partial-blank 语义**：任一列空，**整行 abort**。

创作时要根据目标 list repo（如 `LAF_blocklist`、`LAF_appeal_acceptlist` 等）的 `listRepoAttr` 选对模式，并保证选用的列与 `fieldDef` 一致。

## 字段精确匹配契约

UI 的 EN/ZH tooltip 已明确：
- `verifyRisk` 请求 `eventBody` 中的 **payload 字段名必须与 list repo 列字段名完全一致**。
- **大小写敏感**，**没有自动映射**。
- 字段名错配是规则不 fire 或写入失败的常见原因 → 见 [[risk-troubleshooting-checklist]]。

## 元数据字典

### `bigdata_list_repo`
- 定义每个 list repo 的 `listRepoAttr`（`oneRow` / `mostRow`）和 `fieldDef`（mostRow 列定义）。
- 列上限 3。

### `bigdata_system_dic`
- `addListRepos`：合法的 `repoNo` 白名单；非法 `repoNo`（如被篡改的 POST）须被拒绝。
- `listRepoFieldType`：oneRow 模式下可用字段类型集合，驱动 UI 字段下拉。

## 创作产出

- 一条规则按 `oneRow`、一条按 `mostRow`，分别挂到自有测试 Strategy 下，保存为 **`DRAFT`**。
- 能解释：为什么所选目标 list repo 与列模式匹配、为什么所选列在该 repo 的 `fieldDef` 下合法。

## 相关页面

- 整体架构与事件落库：[[risk-system-architecture-overview]]
- 草稿之后的状态机与审计：[[risk-visual-rule-activation-workflow]]
- 触发与验证操作：[[risk-rule-firing-and-verification]]
- 触发接口：[[api_grc_verify_risk]]
- 缓存与 Kill Switch：[[risk-cache-clear-and-killswitch]]
- 不 fire 时自查：[[risk-troubleshooting-checklist]]
