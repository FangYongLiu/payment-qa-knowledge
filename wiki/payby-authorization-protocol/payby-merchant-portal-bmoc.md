---
title: PayBy商户控台(BMOC)概览
domain: payby-authorization-protocol
kind: wiki_page
slug: payby-merchant-portal-bmoc
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:641f1e44-30b7-40b9-83e9-dba7b4be764a
tags: []
---

# PayBy商户控台(BMOC)概览

PayBy商户控台（BMOC）是 PayBy 面向运营人员的后台管理系统，用于商户入驻、审批与日常管理。本页基于 `Merchant Management` 界面，介绍 BMOC 的导航结构与商户管理列表。

## 访问入口

- 域名示例：`sim-admin.corp.test2pay.com/bmoc/`
- 顶部信息栏：语言切换（English）、消息通知、登录用户名

## 左侧导航结构

BMOC 采用分组式侧边导航，主要分组如下：

- **Basis**
- **Basis Merchant**
- **GENERAL**
- **BUSINESS**
  - **Merchant**
    - Merchant Onboarding
    - Merchant Management
    - Application Approval
    - Tax Info Approval
    - Staff Management
    - Store Management
    - Cashier Management

## Merchant Management 页面

进入 `BUSINESS → Merchant → Merchant Management`，主区域以 Tab 形式展示（`Home` / `Merchant Management`）。

### 筛选条件

页面顶部提供以下筛选项与 `Search` 按钮：

- Merchant ID
- Agent Mid
- Referrer Mid
- Merchant Name
- All Status（状态下拉）
- All Type（类型下拉）
- All Source（来源下拉）
- All Block Flag（封禁标记下拉）

### 商户列表字段

数据表展示商户申请与状态信息，主要列包括：

- Apply ID
- Source（来源，如 `PORTAL`）
- Merchant#（商户号）
- Merchant Name
- MCC
- Business Address
- Signatory Phone
- TPA Name
- TL Expiry（营业执照到期日）
- Application Date
- Status
- Block Flag
- Aplus A...（Aplus 相关字段）
- 操作列

示例行：Apply ID `1443457`、Source `PORTAL`、Merchant# 以 `2000004` 开头、Merchant Name `TestABC`、MCC `7623`、Signatory Phone `+971-05...`、TL Expiry `2027-02...`。
