---
title: 人工资金调拨总览
domain: manual-fund-settlement
kind: wiki_page
slug: manual-fund-settlement-overview
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:b50bca5c-c1e2-439d-bb3e-778735718363
tags: []
related_services:
  - svc_counter
  - svc_h2h
  - svc_reconciliation
related_tables:
  - tbl_reconciliation_t_settlement_detail
  - tbl_reconciliation_t_settlement_template
---

# 人工资金调拨总览

人工资金调拨为清算团队提供统一的账户结算入口，覆盖模板配置、申请审核与系统调拨全流程，规范化操作凭证与审批记录。

## 背景

- 业务资金场景日益丰富，清算团队需登录多个 portal 完成资金划拨。
- 现状存在的问题：
  - 资金划拨记录不统一
  - 操作复杂
  - 流程不规范
- 解决方案：建设统一的账户结算入口，由清算团队对资金账户进行统一结算操作，并规范化操作凭证与审核流程。

## 相关需求来源

- **FAB 0040 AED 账户出款**：Counter settlement function
- **FAB 0062 USD 账户出款**：0062 美元 H2H 出款以及账户登账需求
- **ENBD CMA AED 账户出款**：ENBD Transfer and Reconciliation、ENBD 二期-余额调节

## 整体流程

统一资金调拨包含三个主要环节，端到端步骤详见 [[flow_manual_fund_settlement]]。

### 1. 创建结算模板

入口：counter — settlement management — settlement Template

步骤：选择结算类型 → 填写相关出款账户信息 → 提交审核 → 审核通过。

模板覆盖的结算类型（`settlementType`）、产品码与适用场景说明详见 [[settlement-template-config]]。

### 2. 发起结算申请

入口：counter — settlement detail — apply settlement

步骤：选择模板 → 输入金额 → 提交审核 → 审核通过 → 系统调拨。

Settlement Detail 页面提供以下能力：

- **筛选工具栏**：按业务类型（如 `CA向CA内部`）、`Status`、时间范围（`YYYY-MM-DD HH:mm:ss`）检索结算记录；点击 **Apply Settlement** 按钮发起新的结算申请。
- **结算记录表**核心字段：
  - 业务类型 / Settlement No / Settlement Type（如 `MANUAL`）
  - Voucher、Settlement Amount、Settlement Currency（如 `AED`）
  - Target Account、Fee Amount、File Url
  - Operator、**Audit Status**（如 `PASS`）、**Settlement Result**（如 `SUCCESS` / `FAIL`）
  - Result Code/Msg（失败时回填，如 `FTD-06...`）、Memo、Create/Update 时间
  - Action：支持 `Update Status` 操作

### 3. 系统资金调拨

按结算类型生成对应的账务流水（DR/CR），覆盖 FAB 0040、FAB 0062 出款及 CMA 账户互转等场景，详见 [[settlement-fund-flow]]。

## 关键概念

- **settlementType**：结算类型，非配置项，代码写死枚举（如 `INNER ACCOUNT`、`MERCHANT_ACCOUNT`）。
- **biz_product_code**：业务产品码，与 `settlementType` 配合标识具体调拨场景。
- **settlement_code**：CMA 账户间互转需要额外配置的标识（如 `CMA3->CMA4`）。
- **Audit Status**：申请审核状态（如 `PASS`）。
- **Settlement Result**：系统调拨结果（如 `SUCCESS`、`FAIL`），失败时附带 Result Code/Msg。
- **核心数据表**：
  - `reconciliation.t_settlement_template`
  - `reconciliation.t_settlement_detail`
