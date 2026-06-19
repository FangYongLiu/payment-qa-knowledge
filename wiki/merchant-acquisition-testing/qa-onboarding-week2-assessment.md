---
title: QA入职第二周评估指南
domain: merchant-acquisition-testing
kind: wiki_page
slug: qa-onboarding-week2-assessment
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:AQ/1939439636
tags: []
---

# QA入职第二周评估指南

本页用于指导新QA成员完成入职第二周的评估，目标是验证其对标准QA工作流的理解，并能参与从测试用例设计到生产发布的完整交付生命周期。

## 评估目的

- 验证新QA成员掌握标准QA工作流
- 验证其能够参与完整交付生命周期：从测试用例设计到生产发布

## 评估说明

- 任务应在最少指导下完成
- 所有工作必须记录到对应工具（JIRA / Zephyr）
- 需要提供证据（链接、截图、ticket ID）
- 由 Mentor 进行评审并给予反馈

## 任务 1 — 在 Zephyr 中创建测试用例

**目标：** 展示设计和编写测试用例的能力

**要求：**
- 在 Zephyr 中为指定功能创建测试用例
- 遵循团队的测试用例模板与标准
- 包含清晰的 preconditions、steps、expected results 和 test data
- 将测试用例关联到对应的 JIRA story/task

**完成记录字段：**
- Zephyr Test Cycle
- Test Case IDs / Links
- Reviewer Comments (if any)

## 任务 2 — Bug 报告与跟踪

**目标：** 展示提交高质量缺陷的能力

**要求：**
- 执行测试用例并识别至少一个问题（真实或模拟）
- 按团队 bug 模板在 JIRA 中提交 bug
- 包含 reproduction steps、expected vs actual result、environment、logs/screenshots
- 跟踪 bug 在工作流中的状态变化

**完成记录字段：**
- Bug Ticket ID
- Severity / Priority
- Final Status
- Evidence

## 任务 3 — JIRA 工作流参与

**目标：** 理解 ticket 生命周期与状态流转

**要求：**
- 参与一个 JIRA task/story 的完整生命周期，包括：
  - Requirement review
  - Test preparation
  - Execution
  - Verification
- 按团队工作流恰当地更新 ticket 状态
- 添加有意义的评论，记录测试进展

**完成记录字段：**
- JIRA Ticket ID
- Lifecycle Participation Summary

## 任务 4 — 端到端发布流程参与

**目标：** 体验完整的部署与发布过程

**要求：** 在 Mentor 指导下参与端到端交付流程，包括：
- 代码部署到测试环境
- 测试执行与结果汇报
- 修复验证（如适用）
- 发布准备
- 生产环境部署的观察或参与

**完成记录字段：**
- Feature / Release Name
- Environment(s) Tested
- Key Activities Performed
- Issues Found (if any)

## 自我评估（由新QA成员完成）

简要总结对 QA 流程与发布工作流的理解。

## Mentor 评估（由 Mentor 完成）

**Overall Result 三选一：**
- Pass
- High Risk
- Fail

并填写 Mentor Comments。

## 评估证据要求

每项任务的完成都需提供可追溯的证据：
- JIRA / Zephyr 中的链接或 ticket ID
- 截图、日志等附件
- 评审人或 Mentor 的评论
