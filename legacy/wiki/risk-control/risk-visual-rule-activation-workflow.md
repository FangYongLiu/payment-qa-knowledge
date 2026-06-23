---
title: Visual Rule激活与生效流程
domain: risk-control
kind: wiki_page
slug: risk-visual-rule-activation-workflow
status: archived
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:AQ/2161541121
tags: []
---

# Visual Rule激活与生效流程

本页描述一条 Visual Rule 从 `DRAFT` 到 `ENABLED` 真正生效所经过的状态机、等待窗口、职责分离要求与审计记录产出。

## 状态机全流程

完整路径（系统强制顺序）：

1. `DRAFT` — 在 Visual Rule UI 上保存初稿（参见 [[risk-visual-rule-authoring-guide]]）
2. 点击 **TRIAL** — 进入试运行模式
3. 等待 **≥1 min**（系统强制最短等待）
4. 点击 **Enabled** — 提交评审（submitted for review）
5. 另一名操作员通过 AstraShield 上的 **Audit Record** 审批
6. 状态变为 `ENABLED`
7. 等待 **~35 s** 让缓存重载完成 → 规则真正 live

合计预期等待窗口：**~1.5 min 自计时 + 审批人耗时 + 35 s 缓存重载**。

## Trial 模式语义

- Trial 模式短路在 **rule-level** 与 **strategy-level** **独立生效**（两级各自判断）
- Trial 模式下规则会写一条日志，但 **不会执行 action**
- 验证 Trial 行为：通过列表仓（list repo）中**没有写入新行**来确认（参考 [[risk-rule-firing-and-verification]]）

## 职责分离（Segregation of Duty）

- 谁能审批自己提交的规则 vs 不能 — **按产品域不同**
- `MLIMIT` 类管控下互斥规则更严格（不允许自审）
- 审批动作落在 AstraShield **Audit Record** 上，可作为合规留痕证据

## Audit Record 与 Memo

- 审批通过后产出 Audit Record，可在 AstraShield 上截图留档
- 规则被 `verifyRisk` 事件命中后，事件文档/列表仓行的 audit memo 格式为：
  ```
  from visual rule, eventId=<id>
  ```
- `eventId` 取自 **请求 header**，**不是** body（详见 [[risk-rule-firing-and-verification]]）

## 上线后的验证与回滚

- 走完 `ENABLED` 后须等 ~35 s 缓存窗口；若立刻测试可能因缓存未刷新而看似未生效 → 见 [[risk-cache-clear-and-killswitch]]
- 如规则未按预期生效，先按 [[risk-troubleshooting-checklist]] 自查（rule state / strategy version / checkpoint / 字段匹配 / 缓存）
- 回滚路径（按 blast radius 排序）：
  - Visual Rule UI 上 disable 规则
  - 或翻转 `aml.t_system_param` 运行时开关 + 执行缓存清理
- Kill switch 需 **Tomcat restart**，非热加载，重启后再验证

## Evaluation Gate（本环节通过标准）

- 能把一条规则从 `DRAFT` 一路走到 `ENABLED`
- 知道各阶段预期等待窗口（~1.5 min 自计时 + 审批人 + 35 s 缓存重载）
- 端到端激活一条规则，并产出对应的 **Audit Record 截图**

## 相关页面

- 规则创作前置：[[risk-visual-rule-authoring-guide]]
- 激活后触发与 DB 验证：[[risk-rule-firing-and-verification]]
- 缓存与 Kill Switch：[[risk-cache-clear-and-killswitch]]
- 接口契约：[[api_grc_verify_risk]]
- 系统全景：[[risk-system-architecture-overview]]
