---
title: PRD Review · Salary Card Mono-badge & Co-badge · 2026-05-13
domain: ppc-card-business
kind: wiki_page
slug: prd-review-salary-card-mono-cobadge-2026-05-13
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki
source_ref: wiki:418fe9fe-69f8-48dc-8524-7882ac27ea96
tags: []
---

# PRD Review · Salary Card Mono-badge & Co-badge · 2026-05-13

本页是 Salary Card 双 program PRD（Jaywan Mono + MC×Jaywan Co-badge）的 KB-anchored 完整评审记录，Verdict **Needs Revision**。

## 元信息

| 字段 | 内容 |
|---|---|
| 版本 | Confluence page v16 · last edit 2025-12-24 |
| Review date | 2026-05-13 |
| 来源 | Confluence personal space `~7120206eabd307be494eb09b87ee6105615f36` |
| PRD owner | accountId `712020:6eabd307-be49-4eb0-9b87-ee6105615f36` |
| Reviewer | Can Wang + AI (Claude) |
| Review 类型 | KB-anchored full review (skill `prd-review-PPC`) |
| Verdict | **Needs Revision** |

## 参考的 KB 页

全量加载：
- 二. 资损红线清单（RL-001~030）
- 四. 易错模式清单（重点 EP-001/005/007/008/009/010/018/019/020/022）
- 二. 卡组织规则差异 MC vs Jaywan（Salary Card×Jaywan 列原标 "TBD"）
- 二. 限额体系（MC/PR 全费率表，多币种合并口径待确认）
- 五. 现有 Zephyr 用例索引（PAYM-T3987~T4002 旧版 14 条 / PAYM-T9650~T9657+T9850 P0 Draft）

加载但缺内容：
- 三. 卡组织接口（仅骨架页）
- 四. 历史 Bug 库（PPC-Jaywan 23+ 条；MC×Jaywan co-badge / UAESWITCH / BIN routing 全新）

Skipped：卡生命周期状态机、业务主流程图、监管合规、关键表与字段、异步事件、上下游依赖图、测试卡资源、金额边界值集、MCC 测试集、环境差异表。

## Executive Summary

业务方向清晰（150K cards、80/20 配比、节约 400K AED、CBUAE Mandate 2026-03-31），但 PRD 结构与质量严重不足：21 个标准章节只覆盖 ~7 个，没有 FR 编号 / 没有 Edge Cases / Risks / Rollout / Testing Strategy 实质内容，编号体系自身冲突（两个 `## 3)`）。

KB 视角最大风险：
- **EP-019 BIN 路由错配**（最大单点风险）
- **RL-001~008** 多币种利润核算
- **RL-014~017** Auth-Clearing 不一致
- **RL-024** Force Post
- **RL-026** 对账文件解析

Salary Card × Jaywan 在 KB 中之前标 "TBD"，本 PRD 落地后须反哺 KB。

## Completeness Score

| Category | Score | Notes |
|---|---|---|
| Structure | 7/21 sections | 缺 Goals / Non-Goals / Target Users / User Stories / FR-NFR-Compliance 拆分 / Data / API / UI / Communication / Edge Cases / Dependencies / Risks / Migration / Success Metrics / Timeline / Open Questions / Glossary |
| Requirements clarity | 0/N FRs | 无 FR-NN，无 AC |
| PPC domain coverage | Gaps | 卡组织差异/路由 OK；缺状态机校验、Tokenization lifecycle、Force Post、对账兜底 |
| Test strategy | Insufficient | §6 仅 6 条 must-pass 主流程 |
| Risk coverage | Insufficient | 无 Risks 章节 |
| **Overall** | **Needs Revision** | 早期 draft，可指导 high-level 设计但不能作为开发/测试输入 |

## Critical Issues 🔴

1. **章节编号冲突**：两个 `## 3)`（Detailed Transaction Flows / Clearing, Settlement Ledger），下游 "3.x" 引用无法解析。
2. **无 FR-NN + AC**：开发/QA 都无法逐条对照。
3. **缺 Risks / Edge Cases / Rollout / Migration / Timeline**：CBUAE Mandate 2026-03-31 是硬截止但无阶段计划。
4. **EP-019 BIN 路由错配未对应**：§2.1 引入 `SALCOB / SALMOB` + `t_card_bin` 路由，但缺 ① 灰度/canary ② 错配检测 ③ rollback。
5. **资损红线完全未覆盖**：跨境消费触发 RL-001~RL-008；MIP 路径触发 RL-014~RL-017；新 ledger 触发 RL-026。§3.2 Posting Engine 仅 "keep amount in pending"，对账失败兜底/退款双扣全缺。
6. **Mono 卡 hard-fail 国际交易细节缺**：§3.3 写 "Mono must hard-fail intl. txn"，但未说判定字段（currency != AED？acquiring country？BIN？）、错误码、用户文案、是否记账。

## Warnings 🟡

- 限额数值与 KB 限额体系页冲突 / 待对齐（ATM 3,000 / POS-Ecom 10,000；KB 标 TBD）。
- **Tokenization 双 DPAN lifecycle 错配**：PAN suspended/closed 时两 DPAN 是否一并 revoke 未说。
- 3DS 双 ACS 风险规则差异未说。
- 新 ledger 命名（"jaywan pre-settlement / Jaywan Pending"）与 KB §4 资金账户命名（Customer Basic / Pending / Merchant Pending / Basic / Profit / Shortfall）不齐。
- §6 Test Matrix 仅 must-pass，无反向。
- §7 依赖（BPS / PPC / YSE / EDC / Botim App / Corporate Management）无 owner / status / 关键路径。
- Glossary 缺：CAA / CPV / IHC / IPM / MIP / UAESWITCH / proxy_no / NARADA / SVF。

## Strengths 🟢

- 业务目标量化：150K / 80-20 / 400K AED / 2026-03-31。
- §3.3 Auth Router 规则清晰（SAL_JAY_MONO / SAL_CO_BADGE）。
- §3.1 五段式（Customer→Acquirer→UAESWITCH→Jaywan→YSE→PPC）端到端可读。
- §3.2 国际跨境归 MC 既有框架，避免重复定义。
- §3.1 Posting Engine 双 ledger 区分思路对（虽命名与 KB 不齐）。

## PPC 域分析

| 维度 | 评估 |
|---|---|
| Product scope | 清楚 — Salary Card only，Mono / Co-badge 边界明确 |
| Card scheme scope | 清楚 — Mono=Jaywan / Co-badge=MC+Jaywan |
| Scheme 差异化 | 部分到位（§3.3 / §3.1）；缺 3DS 风险规则、Token lifecycle、Chargeback 窗口、Force Post |
| BIN routing | 引入 `t_card_bin` +
