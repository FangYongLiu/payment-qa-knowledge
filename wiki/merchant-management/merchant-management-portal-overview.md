---
title: 商户管理与控台模块总览(占位)
domain: merchant-management
kind: wiki_page
slug: merchant-management-portal-overview
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:38cad30b-8ceb-496d-ac46-4d0dc2809fcb
tags: []
---

# 商户管理与控台模块总览(占位)

本页是 Merchant Management & Portal 模块的骨架占位，记录商户接入、配置与控台管理相关的文档框架，内容待补充。

## 文档元信息

- Last updated: 2026-04-13
- Updated by: AI
- 业务域: merchant-management

## 1. Business Flow (业务流程)

- **Overview**: Merchant onboarding, configuration, and portal management operations.
- **Flow Diagram**: To be added
- **Key Business Rules**:
  - 商户配置变更通过 General Audit（通用审核）流程进行管控：变更先生成 Audit Record，由审核人在控台执行 Audit 操作后才生效。
  - 收支分离商户场景下，商户参数（如 `ParamKey=fee_b`）的修改纳入审核记录，关联 `MerchantId` 与 `ParamKey`。

## 2. System Flow (系统流程)

- **System Architecture**: 表头 Service/App | Role | Database — To be added
- **后台控台 (PAYBY BASIS)**: 提供商户配置与审核入口，主要导航分组：
  - Data Config：Gateway Config
  - Merchant Config：BlackWhite List、Merchant Setting
  - General Audit：Audit Record、Audit Log
  - 其他模块：Calculation Config、BILL、UFS、International、SqlMonitor、UnityCode Mapping、Open Auth、Query Config、User Resource、Business Monitor、Member Config、Mns Management、Cashier Auth、Protocol Config、Benefit、WPS、Product Mgt、INTEGRATED QUERY
- **API Call Chain**: To be added
- **Key Database Tables**: 表头 Table | Database | Purpose — To be added

## 3. How to Test (测试方法)

- **Test Environment**: PAYBY BASIS 后台控台
- **Test Approach**:
  - 通过左侧导航 General Audit → Audit Record 进入审核记录列表。
  - 列表支持按 `AuditId` 搜索与排序，分页默认 10 articles/page。
  - 每条记录提供 `View` 操作；待审核记录额外提供 `Audit` 按钮触发审核弹窗。
- **Key Test Points**:
  - Audit 弹窗中 `AuditInfo` 区域字段（`MerchantId`、`ParamKey` 等）只读展示，确认与提交变更一致。
  - 验证收支分离商户参数（如 `fee_b`）变更后能正确生成 Audit Record。

## 4. Test Cases (测试用例)

- **Test Case Summary**: 表头 ID | Title | Priority | Type | Status — To be added

## 备注

本页为占位骨架，后续将按上述四大章节补充具体内容。当前已补充 General Audit（Audit Record / Audit Log）入口及收支分离商户参数审核相关信息。
