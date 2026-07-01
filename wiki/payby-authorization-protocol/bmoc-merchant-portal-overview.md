---
title: BMOC商户控台(Merchant Portal)概览
domain: authorization-protocol
kind: wiki_page
slug: bmoc-merchant-portal-overview
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:bde8cda5-9ae7-4415-89c6-dfbad27a7343
tags: []
related_services:
  - svc_aml
  - svc_basis_merchant
  - svc_basis_portal
  - svc_kyc
  - svc_merchant
  - svc_onboarding
---

# BMOC商户控台(Merchant Portal)概览

BMOC（Basis Merchant Onboarding Console）是商户入驻与管理的后台系统，提供商户申请、审批、门店与收银员管理等能力。访问地址形如 `sim-admin.corp.test2pay.com/bmoc/`。

## 左侧导航结构

顶部分组：
- **Basis**
- **Basis Merchant**
- **GENERAL**
- **BUSINESS**

`BUSINESS > Merchant` 子菜单：
- Merchant Onboarding
- Merchant Management
- Application Approval
- Tax Info Approval
- Staff Management
- Store Management
- Cashier Management
- Reconciliation

## Merchant Onboarding 列表页

页面顶部为筛选条与新建入口。

**筛选字段：**
- Merchant ID
- Agent Mid
- Merchant Name
- Awaiting Approval（状态下拉）
- All Type
- All Source
- All Service

**操作按钮：** `Search`、`+ New Merchant`。

## 列表字段

表格列：
- Apply ID
- Source
- Merchant ID
- Merchant Name
- Business
- Signatory / Phone
- Service
- Application Date
- Application Status
- Compliance（合规相关字段）
- 操作列

示例行：Apply ID=2798，Source=PORTAL，Merchant Name=ADCB POS，Service=ACQUIRE，Application Status=Awaiting Approval。

## 审批操作入口

每行操作列提供以下按钮：
- **View**：查看商户申请详情
- **AML Risk Calc**：AML 风险计算
- **KYB Approval**：KYB 审批
- **MCC Confirm**：MCC 确认

页面通过 "Step 1" / "Step 2" 标注审批工作流的执行顺序。

## 其他

- 语言切换：English
- 顶部含通知中心与当前登录用户信息
