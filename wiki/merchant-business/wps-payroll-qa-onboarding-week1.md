---
title: Week 1 - 基础与WPS入门(Guided)
domain: merchant-business
kind: wiki_page
slug: wps-payroll-qa-onboarding-week1
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:AQ/2252570627
tags: []
---

# Week 1 - 基础与WPS入门(Guided)

第一周聚焦账号开通、WPS 业务基础学习与数据库/状态校验，并在导师带领下走完一个 Jira 工单的完整 QA 流程。整体节奏参见 [[wps-payroll-qa-onboarding-plan]]。

## 本周目标

- 完成所有 QA 必备账号与权限的开通。
- 理解 WPS Payroll 业务基础（四大核心流程）。
- 熟悉相关数据库表与状态校验方式。
- 在引导下完成一个 Jira 工单循环：写用例 → 评审 → 一起走完整流程。

## 等待权限期间 (Day 1–2)

可立即开展的知识学习任务：

- **WPS Knowledge Base**：阅读公司注册 (company registration)、发票配置 (invoice configuration)、加员工 (add employee)、创建工资单 (create payroll)、公司管理 (company management)。
  - 产出：能用自己的话描述 WPS 四大核心流程。
  - 联系人：Xinwei Cao
- **Key actors**：理解 YSE（通过 PPC）、CBUAE 的角色与分工。
  - 产出：能解释整条 disbursement chain 上谁负责什么。
  - 联系人：Xinwei Cao
- **Existing work**：阅读近期已完成功能的 Zephyr 测试用例；通读 1–2 个历史 Jira 工单（requirement → cases → execution → closure）。
  - 产出：理解团队的测试用例风格、粒度与工单生命周期。
  - 联系人：Xinwei Cao

## Day 1 — 团队介绍与账号开通

- **Team introduction**：与 QA / Dev / Product / PM 关键联系人见面，能识别 QA、Dev、Ops、PM 的主要对接人。联系人：Xinwei Cao。
- **Account & access**：开通 Jira、Zephyr、Confluence、BMOC（SIM/UAT）、WPS portal、DB 工具访问；并授予 `basis-merchant` 菜单权限。负责方：Ops。
- **Environments**：理解 SIM 与 UAT 的区别及各自用途，明确测试时该使用哪个环境。联系人：Xinwei Cao。

## Day 2–5（权限到位后）— Guided 工单循环

按以下顺序在导师陪同下完整走一遍：

1. **Full-process walkthrough**：导师带你走完一个工单——读需求 → 在 Zephyr 写用例 → 关联工单 → 执行 → 提 bug → 关闭。目标：理解一个真实工单上的端到端 QA 流程。
2. **Write test cases**：为分配的工单独立编写测试用例，覆盖主流程与边界场景。
3. **Review**：与导师一起评审用例，关注覆盖度、边界场景、状态/字段准确性、与需求的一致性，完成修订并通过。
4. **Execute**：在指导下执行用例，按需提 bug 并闭环。

## 通过标准（Week 1）

- 能用自己的话解释 WPS 的四大核心流程。
- 完成并通过评审一个工单量级的测试用例，并执行到位。
- 知道如何在相关数据库表中校验记录，知道日志在哪里查。

## 下一步

通过本周后进入 [[wps-payroll-qa-onboarding-week2-week3]]，开始半独立带工单直至独立交付与发布。
