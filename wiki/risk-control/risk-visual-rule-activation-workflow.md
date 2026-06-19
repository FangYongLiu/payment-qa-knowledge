---
title: Visual Rule 激活与审批流程
domain: risk-control
kind: wiki_page
slug: risk-visual-rule-activation-workflow
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki
source_ref: wiki:00c6a300-c75b-4c5d-b0c9-c18e010dfb50
tags: []
---

# Visual Rule 激活与审批流程

Visual Rule 从草稿到生效需经过状态机流转、审批人复核与缓存重载等待，期间还存在 Trial 模式短路与多层缓存的特殊行为。本页聚焦激活链路本身，规则编写参见 [[risk-visual-rule-authoring-guide]]，触发与验证参见 [[risk-verifyrisk-firing-and-verification]]。

## 状态机全流程

完整链路（单条规则）：

1. `DRAFT` —— 在 [[auto_basis_visual_rule_admin]] 中编写完成后保存。
2. 点击 **TRIAL** —— 进入试运行状态。
3. **等待 ≥ 1 分钟**（系统强制窗口）。
4. 点击 **Enabled** —— 提交审核。
5. **另一名操作员**通过 AstraShield 的 **Audit Record** 完成审批。
6. 状态变为 `ENABLED`。
7. **等待约 35 秒** 完成缓存重载，规则才真正对线上事件生效。

预期等待窗口合计：约 **1.5 分钟自身耗时 + 审批人耗时 + 35 秒缓存重载**。

## 职责分离（Segregation of Duty）

- 审批必须由**非提交者**在 AstraShield Audit Record 完成。
- "能否审批自己提交的规则" 视产品域而异。
- **MLIMIT 类管控**下的互斥规则更严格。

## Trial 模式短路机制

- Trial 模式下规则会写一条日志，但**不执行 action**（例如不会真正写入 list repo）。
- 验证 Trial 状态规则的方式：检查目标 list repo **没有出现新行**。
- Trial-mode 短路在**规则级别**和**策略级别****各自独立**生效，二者互不影响。

## 缓存重载

- `ENABLED` 后约 35 秒缓存自动重载，规则才真正生效。
- 若需手动刷新（运行时参数变更等），见 [[risk-verifyrisk-firing-and-verification]] 中的 Cache Clear 流程；仅在 Risk Param 页面点 Save 是**不够的**。

## Kill Switch 与回滚

回滚路径按爆炸半径排序：

- **UI 禁用规则**：在 Visual Rule 页面直接 disable，颗粒度最小。
- **翻转 `aml.t_system_param` 运行时开关 + 缓存清理**：影响范围更大。
- **Apollo YAML kill switch**：需要 **Tomcat 重启**，**不可热加载**；重启后才能验证生效。

## 交付物与验收

- 能把一条规则从 `DRAFT` 一路推到 `ENABLED`。
- 知道每段等待窗口的预期时长。
- 端到端激活一条规则，并产出对应的 **Audit Record 截图**。
- 能口述上述回滚路径并按爆炸半径排序。

## 相关页面

- 规则与策略层级：[[risk-visual-rule-hierarchy]]
- 规则编写细节：[[risk-visual-rule-authoring-guide]]
- 触发与 DB 验证：[[risk-verifyrisk-firing-and-verification]]
- 系统架构背景：[[risk-system-architecture-overview]]
- 后台入口：[[auto_basis_visual_rule_admin]]
