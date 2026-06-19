---
title: 商户管理与控台模块总览
domain: merchant-business
kind: wiki_page
slug: merchant-management-portal-overview
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:AQ/997818451
tags: []
---

# 商户管理与控台模块总览

本页汇总 Payby 商户端系统的整体结构、业务模块与常用控台入口，帮助新同事快速建立认知，便于后续开展测试工作。所属业务域见 [[domain_merchant_business]]。

## 文档元信息

- Last updated: 2026-04-13
- Updated by: AI
- 业务域: merchant-business

## 1. Business Flow (业务流程)

### Overview

Payby 商户端系统是支付体系中的核心部分，面向各类企业商户（线上电商平台、线下零售店、收银系统集成商等），提供：

- 交易收款（Acquire）
- 账单管理
- 账户管理
- POS 设备接入
- 出款结算（FundOut）
- 企业发薪（WPS）

### 主要业务场景

- **商户入驻**：商户通过统一控台注册并提交入驻资料，由 BMOC 进行审批与业务开通。
- **商户收单（Acquire）**：商户通过 API 网关、QR、PayLink 发起交易，系统处理收单行为。
- **商户出款（FundOut）**：商户余额提现、转账到 IBAN 或 CardNo。
- **POS 业务**：POS 终端的申请、激活与绑定。
- **WPS 业务**：为企业提供发薪服务。

### Flow Diagram

To be added

### Key Business Rules

To be added

## 2. System Flow (系统流程)

### System Architecture / 模块结构

| 系统名称 | 类型 | 功能说明 | Sim 环境访问地址 | 登录信息 / Memo |
|---|---|---|---|---|
| 商户统一控台 (Unified Portal) | Outer Portal | 商户登录/注册、商户入驻、业务开通（Acquire / WPS） | https://sim-web-unified.test2pay.com/verify/login | Mobile: +971-556579167 / Password: 132580 / Merchant: SimBasisMerchant0628 |
| 业务运营后台 (BMOC - Basis Merchant) | Inner Portal | 商户入驻审批、开通支付产品、管理商户信息与权限、门店管理、资金渠道报备、POS 设备审批 | http://sim-admin.corp.test2pay.com/bmoc/ | 员工域账号/密码登录（账号问题找 OPS: wei.li，角色权限找 QA 添加） |
| 商户收单 (Acquire) | Online Business | 商户通过 API 网关、QR、PayLink 发起交易，系统处理收单行为 | 从统一控台登录，选择 'Payment' 业务 | — |
| 商户出款 (FundOut) | Online Business | 商户余额提现、转账到 IBAN 或 CardNo | 从统一控台登录，选择 'Payment' 业务 | — |
| POS 业务 | Offline Business | POS 终端的申请、激活与绑定 | 从统一控台登录，选择 'Payment' 业务 | — |
| WPS 业务 | Business | 为企业提供发薪业务 | 从统一控台登录，选择 'WPS' 业务 | — |
| Bank 控台 | Business | 定制化控台 | https://sim-cooperation.test2pay.com/ | Account: can.wang@payby.com / Pwd: 1qaz!QAZ |

### 控台关系简述

- **Unified Portal**（外部）：商户侧入口，承载注册、入驻、业务开通及各业务模块（Payment、WPS）的操作面板。
- **BMOC**（内部）：运营/审批入口，处理商户入驻审批、产品开通、权限与门店管理、资金渠道报备、POS 设备审批。
- **Bank 控台**：面向银行合作方的定制化控台。

### API Call Chain

To be added

### Key Database Tables

| Table | Database | Purpose |
|---|---|---|
| To be added | | |

## 3. How to Test (测试方法)

### Test Environment

- Sim 环境为主，访问地址与账号见上文模块结构表。
- BMOC 内部账号需使用员工域账号登录，并由 QA 协助添加角色权限。

### Test Approach

To be added

### Key Test Points

- 商户注册 / 登录 / 入驻流程（Unified Portal）
- 入驻审批与业务开通（BMOC）
- Acquire 收单链路（API 网关、QR、PayLink）
- FundOut 出款（提现、IBAN、CardNo 转账）
- POS 设备申请、审批、激活、绑定
- WPS 发薪流程
- Bank 控台定制化能力

## 4. Test Cases (测试用例)

| ID | Title | Priority | Type | Status |
|---|---|---|---|---|
| To be added | | | | |

## 备注

- 本页为 [[merchant-management-portal-overview]] 的总览入口，各子模块（Unified Portal、BMOC、Acquire、FundOut、POS、WPS、Bank 控台）后续将拆分为独立详细文档。
- 业务域归属：[[domain_merchant_business]]。
