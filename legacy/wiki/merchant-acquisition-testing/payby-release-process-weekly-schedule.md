---
title: PayBy 周度发布节奏与排期
domain: merchant-acquisition-testing
kind: wiki_page
slug: payby-release-process-weekly-schedule
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:99041b82-a9a1-4bd5-8a4c-8907cdec1bb5
tags: []
---

# PayBy 周度发布节奏与排期

PayBy 采用滚动式周度发布节奏，每周并行推进 Release 0、Release 1、Release 2 三个发布批次，覆盖 UAT/PROD 部署、SIM/UAT/PROD 测试与合并截止等关键节点。

## 节奏概览

- 每周从周一到周五为工作日，周六、周日不安排发布活动。
- 三个 Release 滚动推进：当周完成 Release 0 收尾、Release 1 主体发布、Release 2 测试与合并准备。
- 关键活动类型：UAT/PROD DEPLOYMENT、SIM/UAT/PROD TESTING、PROD VALIDATION、DEV Merge to Master (Cutoff Time)、Release scope and Config Review。

## 周一（MONDAY）

- Release 0 - UAT DEPLOYMENT
- Release 0 - UAT TESTING
- Release 1 - SIM TESTING

## 周二（TUESDAY）

- Release 0 - PROD DEPLOYMENT
- Release 0 - PROD VALIDATION
- Release 1 - QA SIM TESTING
- Release 1 - DEV Merge to Master (Cutoff Time)
- Release 1 - Release scope and Config Review

## 周三（WEDNESDAY）

- Release 1 - UAT DEPLOYMENT
- Release 1 - QA UAT TESTING
- Release 2 - QA SIM TESTING

## 周四（THURSDAY）

- Release 1 - PROD DEPLOYMENT
- Release 1 - QA PROD VALIDATION
- Release 2 - QA SIM TESTING

## 周五（FRIDAY）

- Release 2 - QA SIM TESTING
- Release 2 - DEV Merge to Master (Cutoff Time)
- Release 2 - Release scope and Config Review

## 周六与周日（SATURDAY / SUNDAY）

- 不安排发布或测试活动。

## 关键时间节点说明

- **DEV Merge to Master (Cutoff Time)**：每个 Release 的代码合并截止时间，Release 1 在周二、Release 2 在周五。
- **Release scope and Config Review**：紧随 Merge Cutoff 之后进行，Release 1 在周二、Release 2 在周五。
- **PROD DEPLOYMENT → PROD VALIDATION**：上线后由 QA 进行生产验证，分别在周二（Release 0）和周四（Release 1）。

相关：[[payby-release-process-weekly-schedule]]
