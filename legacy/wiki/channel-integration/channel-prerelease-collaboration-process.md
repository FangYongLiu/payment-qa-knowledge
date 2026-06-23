---
title: PayBy渠道发布前Dev-Test-Product协作流程
domain: channel-integration
kind: wiki_page
slug: channel-prerelease-collaboration-process
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki
source_ref: wiki:90d0e5a2-d7f3-4451-9ca3-4c76d0f489ab
tags: []
---

# PayBy渠道发布前Dev-Test-Product协作流程

本流程定义渠道相关功能上线前，从范围对齐到上线就绪检查的六个协作步骤，明确 Dev / QA / PM / PMO 在每一步的职责与产出物（均沉淀到 JIRA）。

## Step 1：Functional Scope Alignment

目标：让所有人清楚要交付什么、要测什么。

- Owners: Dev & QA
- Dev：列出代码改动、新增 API、移除的 endpoint，在 JIRA 描述中补充细节与影响范围。
- QA：定义测试范围和回归集，附上 test cycle 链接。

## Step 2：Test Environment & Smoke Strategy

原则：未在真实渠道沙箱中验证的，不算测过。

- Owner: QA
- Mock 使用范围：仅限于异常路径，或第三方暂不可用的部分。
- Smoke 与正式测试：必须在 **channel supplier's test environment** 中执行，不得使用其他环境替代。

## Step 3：Post-SIM Code-Hardening

提示：SIM 退出后、UAT 开始前，至少预留半天窗口用于代码加固。

- Owner: Dev
- Code review & merge：在 Jira 评论中记录评审时间、参与人、评审结果。
- Config review vs prod：使用独立的 JIRA config 条目记录不同环境的配置项。
- CR validation：在每个 Jira item 上评论 "CR-verified"，高亮环境相关值。

## Step 4：UAT Result & Log Verification

- Owners: Dev（QA 协助）
- QA：建立 Test-case ↔ Order-ID 映射；每个 test cycle 附测试结果；将核心用例结果写入 Jira 评论。
- Dev：对提交的订单数据做业务逻辑校验，在 Jira 评论追加 "verification-passed" 标记。

## Step 5：Product Sign-off

- Owner: Product Manager
- QA：跟进 PM，推动 UAT 按期进行。
- PM：完成功能验收，在 JIRA 评论 "verification-passed"。

## Step 6：Go-Live Readiness Checklist

Owner: PMO。上线前由各角色在 JIRA 上逐项验证并留痕。

| # | 检查项 | Verified by | Evidence |
|---|--------|------------|----------|
| 6.1 | UAT 在 channel-supplier UAT 环境执行完毕 | Dev + QA | Test cycle link |
| 6.2 | Key-Vault 值已注入 | Key Manager | Jira 评论附确认结果截图 |
| 6.3 | 最终 config + CR 值已复核 | Dev | 评论 "config-verified" / "CR-verified" |
| 6.4 | 影响说明 + 生产验证脚本 | Dev + QA + Product | 生产验证计划附在 Jira ticket |
| 6.5 | 监控与告警已启用（失败、SLA 违约） | Dev | 附 Grafana alert export JSON |
| 6.6 | 回滚方案已编写并演练 | Dev + QA + Product | 回滚方案文档附在 Jira ticket |

## 角色职责速查

- **Dev**：影响范围说明、代码加固、配置/CR 复核、监控告警、回滚演练。
- **QA**：测试范围与回归集、Smoke/正式测试在渠道沙箱执行、用例与 Order-ID 映射、推动 UAT。
- **PM**：UAT 验收并在 JIRA 签收。
- **PMO**：负责 Go-Live Readiness Checklist 的整体把关。
