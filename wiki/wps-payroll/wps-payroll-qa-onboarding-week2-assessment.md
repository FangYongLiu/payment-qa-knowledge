---
title: Week 2 Onboarding Assessment - QA考核任务与评估
domain: wps-payroll
kind: wiki_page
slug: wps-payroll-qa-onboarding-week2-assessment
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki
source_ref: wiki:239cc0d5-7086-4401-ab0b-50db8e34d274
tags: []
---

# Week 2 Onboarding Assessment - QA考核任务与评估

本页定义 WPS Payroll QA 新成员 Week 2 的考核内容，用于验证其是否掌握标准 QA 流程，能够独立参与从用例设计到生产发布的完整交付生命周期。

## 考核目的与说明

- **目的**：确认新成员理解标准 QA 工作流，能参与完整交付生命周期（测试用例设计 → 生产发布）
- **完成方式**：
  - 在最少指导下完成各项任务
  - 所有工作记录在对应工具中（JIRA / Zephyr）
  - 提供证据材料：链接、截图、ticket ID
  - 由 Mentor 审阅并反馈

## Task 1 — Zephyr 测试用例设计

**目标**：展示测试用例设计与文档撰写能力。

**要求**：
- 在 Zephyr 中为指派的功能创建测试用例
- 遵循团队测试用例模板与规范
- 用例需包含清晰的：preconditions、steps、expected results、test data
- 将测试用例关联到对应的 JIRA story/task

**完成记录字段**：
- Zephyr Test Cycle
- Test Case IDs / Links
- Reviewer Comments（如有）

## Task 2 — Bug 上报与跟踪

**目标**：展示高质量缺陷报告能力。

**要求**：
- 执行测试用例并发现至少一个问题（真实或模拟）
- 在 JIRA 中按团队 bug 模板提交缺陷
- 提交内容包含：复现步骤、expected vs actual results、环境信息、logs/screenshots
- 跟踪 bug 在工作流中的状态流转

**完成记录字段**：
- Bug Ticket ID
- Severity / Priority
- Final Status
- Evidence

## Task 3 — JIRA 工作流流转参与

**目标**：理解 ticket 生命周期与状态流转。

**要求**：参与完整的 JIRA task/story 生命周期，覆盖以下阶段：
- Requirement review
- Test preparation
- Execution
- Verification

同时需要：
- 按团队工作流更新 ticket 状态
- 添加有意义的评论，记录测试进展

**完成记录字段**：
- JIRA Ticket ID
- Lifecycle Participation Summary

## Task 4 — 端到端发布流程参与

**目标**：体验完整的部署与发布流程。

**要求**：在 mentor 指导下，参与端到端交付流程，包括：
- 代码部署到测试环境
- 测试执行与结果汇报
- 修复验证（如适用）
- 发布准备
- 生产部署观察或参与

**完成记录字段**：
- Feature / Release Name
- Environment(s) Tested
- Key Activities Performed
- Issues Found（如有）

## 自评（新 QA 成员填写）

需提供简要总结，描述对 QA 流程及发布工作流的理解。

## Mentor 评估

**Overall Result**（三选一）：
- Pass
- High Risk
- Fail

**Mentor Comments**：由导师填写评语。
