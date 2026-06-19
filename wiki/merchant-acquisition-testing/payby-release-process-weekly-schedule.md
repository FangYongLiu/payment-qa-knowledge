---
title: PayBy 发布流程周计划
domain: merchant-acquisition-testing
kind: wiki_page
slug: payby-release-process-weekly-schedule
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:59aa7943-f636-4622-a3c2-ce5f0eff6a02
tags: []
---

# PayBy 发布流程周计划

本页描述 PayBy 每周（周一至周五）的发布流程节奏，涵盖 UAT/PROD 部署、SIM/UAT/PROD 测试以及 DEV Merge 截止等关键活动；周六、周日为非工作日。

## 角色与颜色图例

- **灰色 (Grey)** — Devops / DBA
- **蓝色 (Blue)** — QA
- **绿色 (Green)** — DEV

## 周一 (MONDAY)

- Release 0 - UAT DEPLOYMENT（Devops）
- Release 0 - UAT TESTING（QA）
- Release 1 - SIM TESTING（QA）

## 周二 (TUESDAY)

- Release 0 - PROD DEPLOYMENT（Devops）
- Release 0 - PROD VALIDATION（QA）
- Release 1 - QA SIM TESTING（QA）
- Release 1 - DEV Merge to Master (Cutoff Time)（DEV）
- Release 1 - Release scope and Config Review（Devops）

## 周三 (WEDNESDAY)

- Release 1 - UAT DEPLOYMENT（Devops）
- Release 1 - QA UAT TESTING（QA）
- Release 2 - QA SIM TESTING（QA）

## 周四 (THURSDAY)

- Release 1 - PROD DEPLOYMENT（Devops）
- Release 1 - QA PROD VALIDATION（QA）
- Release 2 - QA SIM TESTING（QA）

## 周五 (FRIDAY)

- Release 2 - QA SIM TESTING（QA）

## 周六 / 周日

- 非工作日（greyed out）。

## 节奏要点

- 每周并行推进多个 Release：上一 Release 进入 UAT/PROD 阶段时，下一 Release 已开始 SIM 测试。
- **DEV Merge to Master Cutoff** 固定在周二，作为下一 Release 进入 UAT 前的代码冻结点。
- 周二同步进行 Release scope 与 Config Review，为周三的 UAT 部署做准备。
- PROD 部署集中在周二与周四，部署后由 QA 立即执行 PROD VALIDATION。

## 相关页面

- [[payby-release-process-weekly-schedule]]
