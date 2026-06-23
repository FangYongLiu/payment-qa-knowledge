---
title: PRD 变更日志（模板与索引）
domain: ppc-card-business
kind: wiki_page
slug: prd-review-changelog-template
status: archived
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:AQ/2135621636
tags: []
---

# PRD 变更日志（模板与索引）

本页是 PRD review 归档的**模板与索引页**，本身不存放 review 数据；每次 `prd-review-PPC` skill 跑完会在本页下新建子页承载该次 review 的完整输出。

## 本页用途

- 仅保留**模板字段说明**与**维护规则**。
- 不放具体 review 数据：所有内容由 skill 自动生成的子页承载。
- 维护人：Jianfei Wang｜状态：模板页 / Template page。

## 子页面命名规则

- **格式**：`<需求名> · <YYYY-MM-DD>`
- **示例**：`Salary Card Mono-badge & Co-badge · 2026-05-13`
- 同一份 PRD 多轮 review（v1 / v2 / v3）→ 每轮**新建一个子页**（日期不同自然区分）。
- **不覆盖旧子页**：diff 历史本身有价值。

## 子页内容结构（模板字段）

每个子页按以下字段组织：

| 字段 | 说明 |
| --- | --- |
| 版本号 | 如 v2.5.0 / Confluence page version / GitHub head SHA |
| 发布日期 | YYYY-MM-DD（review 日期，也是子页 title 后缀） |
| PRD 链接 | GitHub PR / Confluence —**必填**，原始需求链接 |
| 变更摘要 | 3~5 个 bullet |
| 影响范围 | 哪些模块（链接到本 KB 的对应页） |
| 风险评估 | `prd-review-PPC` skill 输出，关键风险点每条 cite RL-NNN / EP-NNN / BUG key |
| 评审记录 | 评审会议记录链接（可选） |
| 测试范围 | 回归 / 新增 / 仅冒烟 + 用例数预估 |
| 是否更新 KB | 哪些层 / 哪些页已同步（落地前为 follow-up checklist） |

## 维护提醒

- 每次 PRD review 跑完，`prd-review-PPC` skill 的 **Step 6** 自动创建子页——**不要手动跳过**。
- 子页 title 严格遵循 `<需求名> · <YYYY-MM-DD>` 格式，保证按字母/日期排序时一目了然。
- 同一 PRD 多轮 review **各开新子页**，不要在旧子页基础上覆盖。
- 如果 PRD 影响"二、规则与约束"或"三、技术接口"层，**PRD 落地后必须同步更新对应 KB 页**，并勾掉子页 "Follow-ups" 中对应 checkbox。

## 数据来源

- `prd-review-PPC` skill（自动建子页）
- GitHub PR / Confluence 原 PRD 链接
- 评审会议输出（挂在子页"评审记录"字段）

## 子页面索引

- Confluence 左侧导航会自动列出本页所有子页，按子页 title 排序。
- 最新 review 在最上面（**日期降序**）。
- 如需手动维护汇总表，可在本节追加。
