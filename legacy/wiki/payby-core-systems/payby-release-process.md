---
title: PayBy 发布流程与排期
domain: payby-core-systems
kind: wiki_page
slug: payby-release-process
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:bd27e7d8-aa76-4ea0-923e-bb495f0710b9
tags: []
---

# PayBy 发布流程与排期

PayBy 常规发布窗口为每周二、周四 UAE 时间 06:00。任何在常规发布窗口之外的 Hotfix 部署都必须经过管理团队的严格审批流程。

## 常规发布窗口

- 每周二 06:00 (UAE Time)
- 每周四 06:00 (UAE Time)
- 窗口外的 Hotfix 需走管理团队严格审批

## 周排期

按一周排布两个发布序列（Release 1 与 Release 2），并保留上一周的 Release 0 收尾活动。

**MONDAY**
- Release 0 - UAT DEPLOYMENT
- Release 0 - UAT TESTING
- Release 2 - QA SIM TESTING

**TUESDAY**
- Release 0 - PROD DEPLOYMENT
- Release 0 - PROD VALIDATION
- Release 1 - SIM TESTING
- Release 1 - QA SIM TESTING
- Release 1 - Release scope and Config Review
- Release 1 - DEV Merge to Master (Cutoff Time)

**WEDNESDAY**
- Release 1 - UAT DEPLOYMENT
- Release 1 - QA UAT TESTING
- Release 2 - QA SIM TESTING

**THURSDAY**
- Release 1 - PROD DEPLOYMENT
- Release 1 - QA PROD VALIDATION
- Release 2 - QA SIM TESTING
- Release 2 - Release scope and Config Review
- Release 2 - DEV Merge to Master (Cutoff Time)

**FRIDAY / SA / SU**
- 无固定发布活动

## 角色与职责

**DEVOPS / DBA**
- 负责 UAT 与 PROD 的部署
- 依据 release scoped tickets 中的信息执行：Build Version、CRs、Configuration files 等
- 所有 UAT 部署与配置变更仅限 DevOps 与 DBA 团队执行

**QA**
- 在 SIM、UAT、PROD 进行测试：Functional Testing、Regression、Smoke
- 覆盖手工与自动化两种方式

**DEV**
- 在 DEV 环境完成 Self Tests
- 在 QA 完成 SIM 测试后，将代码合并到 master
- 在发布日按 ticket 维度完成 Release Confirm 任务（见下文）

### Release Confirm 任务

在发布流程中，每个进入当次 release 的 ticket 会生成一条对应的 Release Confirm 任务，由该 ticket 的负责开发人员逐条确认完成。

任务以表格形式跟踪，字段包括：

- **Task**：以 ticket key 命名，例如 `PAYM-1234 Release confirm`、`PAYM-5678 Release confirm`
- **Assigned to**：负责该 ticket 的开发人员（如 Developer 01 / Developer 02）
- **Due date**：通常为发布当天（Today）
- **Bucket**：初始状态为 `To do`，开发完成确认后勾选为已完成（completed，带删除线显示）

## 工作流新增状态

整体流程中新增两个状态，配合"UAT 部署与配置变更仅由 DevOps/DBA 执行"的规范：

- `UAT DB CHANGE`
- `UAT DEPLOY`

## 安全确认流程

针对涉及暴露到公网的核心服务变更的 ticket：

- 在 UAT 完成 QA 验证后，需要将状态切换为 `SECURITY CONFIRM`
- 最终结束状态为 `SECURITY COMPLETED`，而不是普通的 `COMPLETED`

## Definition of Done

- 所有 ticket 已上线 PROD，且状态为 `COMPLETED` 或 `SECURITY COMPLETED`
- 对应的 Release Confirm 任务已由负责开发人员勾选完成
- 部署过程中出现的任何问题都需复盘，分析 root cause，并制定 action items，避免后续重复发生
