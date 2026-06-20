---
title: PRD 变更日志模板与索引
domain: ppc-card-business
kind: wiki_page
slug: prd-review-changelog-template
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki
source_ref: wiki:10af8307-ab2b-4a50-a045-1a3c2bff0511
tags: []
---

# PRD 变更日志模板与索引

本页是 PRD review 归档的**模板与索引页**，本身不承载具体 review 数据，仅定义子页面命名规则、字段模板与维护规则。所属业务域：`ppc-card-business`。

## 本页定位

- 每次 `prd-review-PPC` skill 跑完，会在本页下**自动新建子页**承载该次 review 的完整输出。
- 本页只保留**模板字段说明**与**维护规则**，不放具体 review 内容。
- 子页索引由 Confluence 左侧导航自动呈现，按 title 排序，日期降序在前。

## 子页面命名规则

- **格式**：`<需求名> · <YYYY-MM-DD>`
- **示例**：`Salary Card Mono-badge & Co-badge · 2026-05-13`
- 同一份 PRD 多轮 review（v1 / v2 / v3）→ 每轮**新建子页**，靠日期自然区分。
- **不覆盖旧子页**——diff 历史本身有价值。

## 子页内容结构 / 字段模板

每个子页按以下字段组织：

| 字段 | 说明 |
|---|---|
| 版本号 | 如 v2.5.0 / Confluence page version / GitHub head SHA |
| 发布日期 | `YYYY-MM-DD`，即 review 日期，同时是子页 title 后缀 |
| PRD 链接 | GitHub PR / Confluence —— **必填**，原始需求链接 |
| 变更摘要 | 3~5 个 bullet |
| 影响范围 | 涉及模块，链接到本 KB 对应页 |
| 风险评估 | `prd-review-PPC` skill 的输出，关键风险点每条 cite `RL-NNN` / `EP-NNN` / BUG key |
| 评审记录 | 评审会议记录链接（可选） |
| 测试范围 | 回归 / 新增 / 仅冒烟 + 用例数预估 |
| 是否更新 KB | 哪些层 / 哪些页已同步；落地前作为 follow-up checklist |

## 维护规则

- `prd-review-PPC` skill 的 **Step 6 会自动创建子页**——不要手动跳过。
- 子页 title 严格遵守 `<需求名> · <YYYY-MM-DD>`，保证字母/日期排序时一目了然。
- 同一 PRD 多轮 review **各开新子页，不在旧子页上覆盖**。
- 若 PRD 影响 **"二、规则与约束"** 或 **"三、技术接口"** 层，PRD 落地后**必须同步更新对应 KB 页**，并勾掉子页 "Follow-ups" 内对应 checkbox。

## 数据来源

- `prd-review-PPC` skill（自动建子页）
- GitHub PR / Confluence 原 PRD 链接
- 评审会议输出（挂在子页 "评审记录" 字段）

## 子页面索引

- Confluence 左侧导航自动列出本页所有子页，按子页 title 排序，**最新 review 在最上**（日期降序）。
- 如需手动维护汇总表，可在本节追加。
