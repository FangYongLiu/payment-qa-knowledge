---
title: PayBy渠道发布前Dev-Test-Product协作流程
domain: channel-integration
kind: wiki_page
slug: payby-channel-pre-release-collaboration-process
status: archived
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:AQ/1467416579
tags: []
---

# PayBy渠道发布前Dev-Test-Product协作流程

本页规范PayBy渠道类需求在发布前，从功能范围对齐到上线就绪的6步协作流程，明确每一步的责任人、动作与产出物（Evidence），确保发布质量可追溯。

## Step 1：Functional Scope Alignment（功能范围对齐）

- Owners：Dev & QA
- 目标：所有相关方明确"做什么"与"测什么"。

| 任务 | 责任人 | 产出 / 位置 |
|---|---|---|
| 列出代码变更、新增 API、下线 endpoint | Dev | 在 JIRA 描述中补充细节及影响范围 |
| 定义测试范围 + 回归测试包 | QA | 附上 test cycle 链接 |

## Step 2：Test Environment & Smoke Strategy（环境与冒烟策略）

- Owner：QA
- 核心原则：**未在渠道真实 sandbox 中测试过的，不算测过。**

- **Mock 使用范围**：仅适用于 *异常路径* 或 *第三方暂不可用* 的场景。
- **Smoke run**：冒烟与正式测试均必须在 **channel supplier 的 test 环境** 执行。

## Step 3：Post-SIM Code-Hardening（SIM后代码加固）

- Owner：Dev
- 时间窗口提示：**SIM 退出后、UAT 之前，至少预留半天窗口期**。

| 检查项 | Evidence |
|---|---|
| Code review & merge | 在 Jira 评论中记录评审时间、参与人、评审结论 |
| Config review vs prod | 在 JIRA 用独立配置项记录不同环境的配置 |
| CR validation | 在每条 Jira 评论 "CR-verified"，高亮环境差异值 |

## Step 4：UAT Result & Log Verification（UAT结果与日志验证）

- Owners：Dev（QA 协助）

| 任务 | 责任人 | 产出 |
|---|---|---|
| Test-case ↔ Order-ID 映射 | QA | 每个 test cycle 须附测试结果；将核心 test-case 结果写入 Jira 评论 |
| 业务逻辑 sanity check | Dev | 对提交的订单数据，在 Jira 评论补充 "verification-passed" 标记 |

## Step 5：Product Sign-off（产品验收签收）

- Owner：Product Manager

| 动作 | 责任人 |
|---|---|
| 跟进 PM，推动及时进行 user-acceptance testing | QA |
| 完成功能验收，在 JIRA 评论 "verification-passed" | PM |

## Step 6：Go-Live Readiness Checklist（上线就绪检查）

- Owner：PMO

| # | 检查项 | Verified by | Evidence |
|---|---|---|---|
| 6.1 | 在 channel-supplier UAT 上执行 UAT | Dev + QA | Test cycle 链接 |
| 6.2 | Key-Vault 值已注入 | Key Manager | 在 Jira 评论附确认结果截图 |
| 6.3 | 最终 config + CR 值已 review | Dev | 评论 "config-verified" / "CR-verified" |
| 6.4 | 影响声明 + 生产验证脚本 | Dev + QA + Product | 将 production-validation plan 附在 Jira ticket |
| 6.5 | 监控与告警已启用（失败、SLA breach） | Dev | 附 Grafana alert export JSON |
| 6.6 | 回滚方案已文档化并演练 | Dev + QA + Product | 将 rollback-plan 文档附在 Jira ticket |

## 关键约束速览

- **环境约束**：Smoke 与正式测试一律在渠道供应商测试环境执行；Mock 仅限异常路径或第三方不可用。
- **时间约束**：SIM 退出到 UAT 之间，必须预留至少半天的代码加固窗口。
- **证据约束**：每个步骤的 Evidence 都需落到 JIRA（评论、附件、test cycle 链接、截图、JSON 导出等），便于追溯。
