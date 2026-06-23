---
title: WPS Payroll QA 入职 Week 1 - 基础与 WPS 入门
domain: merchant-business
kind: wiki_page
slug: wps-payroll-qa-onboarding-week1
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki
source_ref: wiki:b9c47ea9-7a47-4cf2-9849-6bc4dfdabc97
tags: []
---

# WPS Payroll QA 入职 Week 1 - 基础与 WPS 入门

第一周以指导式学习为主，目标是搭好账号与环境、建立 WPS 业务认知，并在 mentor 带领下完整跑通一个 Jira ticket 周期。完整三周安排见 [[wps-payroll-qa-onboarding-plan]]。

## 本周目标

- 完成所有 QA 账号与访问权限的开通
- 掌握 WPS 薪资业务基础知识（四大核心流程）
- 熟悉相关数据库表与状态检查方式
- 在指导下完成一个 Jira ticket 周期：写用例 → 评审 → 一起走完整流程

## 访问权限到位前（Day 1–2）

权限仍在开通中，先做可立即开始的知识储备。

- **WPS 知识库阅读**：company registration、invoice configuration、add employee、create payroll、company management；产出能用自己的话描述 WPS 四大核心流程。
- **关键角色理解**：YSE（via PPC）、CBUAE 在发薪链路中的分工；能讲清谁在哪个环节做什么。
- **存量资产学习**：阅读近期已完成 feature 的 Zephyr 测试用例；端到端读 1–2 个历史 Jira ticket（requirement → cases → execution → closure），熟悉用例风格、颗粒度与 ticket 生命周期。
- 联系人：Xinwei Cao。

## Day 1 — 团队与访问设置

| 事项 | 内容 | Owner | 验收 |
| --- | --- | --- | --- |
| 团队介绍 | 认识 QA / Dev / Product / PM 关键联系人 | Xinwei Cao | 能识别 QA、Dev、Ops、PM 关键联系人 |
| 账号与访问 | 开通 Jira、Zephyr、Confluence、BMOC（SIM/UAT）、WPS portal、DB 工具 | Ops | 全部可登录；basis-merchant 菜单权限已授予 |
| 环境认知 | 理解 SIM vs. UAT 各自的用途 | Xinwei Cao | 知道该在哪个环境执行测试 |

## Day 2–5（权限到位后）— 指导式 Ticket 周期

- **全流程 walkthrough**：mentor 带走一遍——读需求 → Zephyr 写用例 → 关联到 ticket → 执行 → 报 bug → 关单。
- **写测试用例**：为分配到的 ticket 起草用例，覆盖主流程与边界场景。
- **用例评审**：和团队一起过覆盖度、边界情况、状态/字段准确性、与需求的对齐；修正后通过。
- **执行**：在指导下执行用例，按需提 bug，闭环关单。

## WPS 业务范围回顾

本岗位聚焦 WPS 薪资发放场景及其背后的集成：

- 公司注册与审批流
- 员工注册（Add Employee）
- 薪资创建与发放（WPS via CBUAE，以及 Direct Transfer）
- 发票/账单核对
- 测试用例编写与 bug 上报
- 涉及集成方：YSE via PPC、CBUAE 文件交换、TradeII

## Week 1 通过标准

- 能用自己的话讲清 WPS 四大核心流程
- 完成并执行了一个 ticket 量级的、已评审通过的测试用例
- 知道如何在相关数据库表中核对记录、在哪里查日志

## 下一步

进入 [[wps-payroll-qa-onboarding-week2]]，由半独立带单过渡。
