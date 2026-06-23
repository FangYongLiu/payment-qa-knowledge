---
title: PRD Review · Salary Card Mono-badge & Co-badge (2026-05-13)
domain: ppc-card-business
kind: wiki_page
slug: prd-review-salary-card-mono-cobadge-2026-05-13
status: archived
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:AQ/2167636024
tags: []
---

# PRD Review · Salary Card Mono-badge & Co-badge (2026-05-13)

本页归档 2026-05-13 对 Salary Card 两个新 program（Jaywan Mono + MC×Jaywan Co-badge）PRD 的 KB-anchored full review。详见上层流程 [[prd-review-PPC-overview]] 与业务总览 [[salary-card-mono-cobadge-overview]]，测试关注点见 [[salary-card-test-watch-points]]。

## 元信息 / Metadata

| 字段 | 内容 |
|---|---|
| 版本号 | Confluence page v16 · last edit 2025-12-24 |
| Review date | 2026-05-13 |
| PRD 链接 | Salary Card Mono-badge & Co-badge: PRD |
| 来源类型 | Confluence personal space `~7120206eabd307be494eb09b87ee6105615f36` |
| PRD owner accountId | `712020:6eabd307-be49-4eb0-9b87-ee6105615f36` |
| Reviewer | Can Wang + AI (Claude) |
| Review 类型 | KB-anchored full review (skill `prd-review-PPC`) |
| Verdict | **Needs Revision** |

## 本次 review 参考的 KB 页 / KB References Used

✅ 全量加载：
- 二. 资损红线清单 (`2134310994`) — RL-001~030 全套
- 四. 易错模式清单 (`2132803779`) — EP-001 / EP-005 / EP-007 / EP-008 / EP-009 / EP-010 / **EP-018 配置漂移** / **EP-019 BIN 路由错配** / EP-020 / EP-022
- 二. 卡组织规则差异（MC vs Jaywan）(`2132803758`) — Salary Card × Jaywan 列原标 "待确认 TBD"
- 二. 限额体系 (`2134966320`) — MC/PR 全费率表，多币种合并口径未确认
- 四. 历史 Bug 库 (`2133131397`) — PPC-Jaywan 23+ 条；BUG-6936 / BUG-7192~7266 / **BUG-7425 Jaywan 卡绑定** / BUG-7429 / BUG-7689 / BUG-7781；MC×Jaywan co-badge / UAESWITCH / BIN routing 历史 bug 搜不到（全新场景）
- 五. 现有 Zephyr 用例索引 (`2134835276`) — 根 1 PAYM-T3987~T4002（Botim 4.0 14 条 Draft 未自动化）；根 3 PAYM-T9650~T9657 + T9850（Jianfei IOS 8 条 P0 Draft）

⚠️ KB 内容缺失：
- 三. 卡组织接口 (`2134835256`) — 骨架页，仅 "内容结构建议"

Skipped intentionally：
- 一. 卡生命周期状态机 (`2133393518`) — PRD 未改状态机，通过 RL-018/RL-019/EP-005/EP-007 间接覆盖
- 一. 业务主流程图 (`2133196989`) — PRD §3 自身就是流程图
- 二. 监管合规 (`2133131377`) — PRD 仅引用 CBUAE/AEP 时间点
- 三. 关键表与字段 (`2134179970`) / 异步事件 (`2134868047`) / 上下游依赖图 (`2134048858`) — 开发评审时建议补读
- 五. 测试卡资源 (`2133328021`) / 金额边界值集 (`2134966340`) / MCC 测试集 (`2133819527`) / 环境差异表 (`2134900794`) — Test Watch Points 中按通用规则覆盖

## Executive Summary

PRD 描述 Jaywan Mono + MC×Jaywan Co-badge 两个 program 的发卡 / 路由 / 清算 / Tokenization / 3DS 改动，**CBUAE Mandate 2026-03-31**。业务方向清晰，但 PRD 结构与质量严重不足：21 个标准章节只覆盖 ~7 个，没有 FR 编号、没有 Edge Cases / Risks / Rollout / Testing Strategy 实质内容，编号体系自身有冲突（两个 `## 3)`）。

最大风险：**EP-019 BIN 路由错配**；**RL-001~008 多币种利润核算** / **RL-014~017 Auth-Clearing 不一致** / **RL-024 Force Post** / **RL-026 对账文件解析** 都被 co-badge 触发，PRD 完全未对应。Salary Card × Jaywan 在 KB 中之前标 "TBD"，本 PRD 落地后必须反哺 KB。

### Completeness Score

| Category | Score | Notes |
|---|---|---|
| Structure | 7 / 21 sections | 缺 Goals/Non-Goals · Business Impact · Target Users · User Stories · Functional/Non-Functional/Compliance 显式拆分 · Data Requirements · API spec · UI/UX（仅 §5 半页）· Communication · Edge Cases · Dependencies（仅 §7 罗列）· Risks · Migration/Rollout · Success Metrics · Timeline · Open Questions · Glossary |
| Requirements clarity | 0 / N FRs | 没 FR 编号，应拆 FR-01 ~ FR-NN + AC |
| PPC domain coverage | Gaps | 卡组织差异/路由 OK；缺：状态机校验、双 Tokenization lifecycle、Force Post、对账失败兜底 |
| Test strategy | Insufficient | §6 只列 6 条 must-pass，无负向/边界/异常 |
| Risk coverage | Insufficient | 完全没有 Risks & Mitigations |
| Overall | **Needs Revision** | 早期 draft，可指导 high-level 设计，不可作为开发/测试输入交付 |

## Detailed Findings

### 🔴 Critical Issues

1. **章节编号冲突**：两个 `## 3)`（`Detailed Transaction Flows` 与 `Clearing, Settlement Ledger`），下游 "3.x" 引用无法解析
2. **没有 FR-NN + AC**：开发/QA 无法逐条对照
3. **缺 Risks & Mitigations / Edge Cases / Rollout / Migration / Timeline**：CBUAE Mandate 2026-03-31 是硬截止
4. **EP-019 BIN 路由配置错误未对应**：§2.1 引入 `SALCOB / SALMOB` + `t_card_bin`，但缺 ① 灰度/canary ② 错配检测 ③ rollback
5. **资损红线完全未覆盖**：RL-001~008（跨境多币种 P&L）、RL-014~017（MIP Auth-Clearing）、RL-026（对账文件解析）；§3.2 Posting Engine 只说 "keep amount in pending"
6. **Mono 卡 hard-fail 国际交易实现细节缺**：判定字段（currency != AED？acquiring country？BIN？）、错误码、用户提示、是否记账，全缺

### 🟡 Warnings

- 限额数值与 KB 限额体系页冲突：ATM 单笔 3,000 / POS-Ec
