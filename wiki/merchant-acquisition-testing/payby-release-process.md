---
title: PayBy 发布流程
domain: merchant-acquisition-testing
kind: wiki_page
slug: payby-release-process
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:AQ/732889111
tags: []
---

# PayBy 发布流程

PayBy 采用每周二、周四 UAE 时间 6:00am 的常规双周发布节奏；窗口外的 Hotfix 必须经管理团队严格审批。

## 发布节奏（周一 ~ 周四）

| 日 | 主要活动 |
|---|---|
| MONDAY | Release 0 - UAT DEPLOYMENT；Release 0 - UAT TESTING；Release 1 - SIM TESTING；Release 1 - Release scope and Config Review |
| TUESDAY | Release 0 - PROD DEPLOYMENT；Release 0 - PROD VALIDATION；Release 1 - QA SIM TESTING |
| WEDNESDAY | Release 1 - UAT DEPLOYMENT；Release 1 - QA UAT TESTING；Release 2 - QA SIM TESTING；Release 2 - DEV Merge to Master (Cutoff Time)；Release 2 - Release scope and Config Review |
| THURSDAY | Release 1 - PROD DEPLOYMENT；Release 1 - QA PROD VALIDATION；Release 2 - QA SIM TESTING；Release 1 - DEV Merge to Master (Cutoff Time) |

> 周五及周末（FRIDAY/SA/SU）无常规发布动作。

## 各角色职责

- **DEVOPS / DBA**：负责 UAT 和 PROD 的部署，依据 release scoped tickets 中的信息执行（Build Version、CRs、Configuration files 等）。
- **QA**：负责 SIM、UAT、PROD 的测试，覆盖 Functional Testing、Regression、Smoke，手工与自动化并行。
- **DEV**：在 DEV 环境完成 Self Tests，并在 QA 于 SIM 完成测试后将代码合入 master。

## 新增状态：UAT DB CHANGE 与 UAT DEPLOY

流程中新增两个状态：

- **UAT DB CHANGE**
- **UAT DEPLOY**

强化要求：所有 UAT 部署与配置变更**只能**由 DevOps 与 DBA 团队执行。

## SECURITY CONFIRM 流转

针对涉及暴露在公网的 core service 变更的工单：

- QA 在 UAT 完成验证后，状态须流转到 **SECURITY CONFIRM**。
- 最终结束状态为 **SECURITY COMPLETED**（而非普通的 COMPLETED）。

## Definition of Done (DoD)

- 所有工单均已上线 PROD，状态变更为 **COMPLETED** 或 **SECURITY COMPLETED**。
- 部署过程中出现的任何问题须进行复盘，分析根因并制定改进 action items，避免同类问题再次发生。
