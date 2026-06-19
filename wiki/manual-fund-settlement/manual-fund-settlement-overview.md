---
title: 人工资金调拨总览
domain: manual-fund-settlement
kind: wiki_page
slug: manual-fund-settlement-overview
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki
source_ref: wiki:11dc5fef-89b3-45ad-81a8-95bfefa0519a
tags: []
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

模板覆盖的结算类型（`settlementType`）、产品码与适用场景说明详见 [[settlement-template-config]]；产品码到具体场景的映射另见 [[settlement-type-product-code-mapping]]。

模板中账户配置入口：Reconciliation Manage — Recon Config。涉及的配置列表：

- **payer List**：`SettlementMerchantPayerInfoList`、`SettlementCB103PayerInfoList`、`SettlementCB001PayerInfoList`
- **beneficiary List**：`SettlementCB103BeneficiaryInfoList`、`SettlementInnerBeneficiaryInfoList`
- **Bank Deposit Account**：`SettlementInnerFundOutBankAccountList`

### 2. 发起结算申请

入口：counter — settlement detail — apply settlement

步骤：选择模板 → 输入金额 → 提交审核 → 审核通过 → 系统调拨。

### 3. 系统资金调拨

按结算类型生成对应的账务流水（DR/CR），覆盖 FAB 0040、FAB 0062 出款及 CMA 账户互转等场景，详见 [[manual-settlement-fund-flow]]。

## 关键概念

- **settlementType**：结算类型，非配置项，代码写死枚举（如 `INNER ACCOUNT`、`MERCHANT_ACCOUNT`）。
- **biz_product_code**：业务产品码，与 `settlementType` 配合标识具体调拨场景。常见值：
  - `INNER ACCOUNT`：`500105`、`500108`、`500109`、`500110`、`500111`、`500113`
  - `MERCHANT_ACCOUNT`：`230601`（AED to AED）、`230602`（AED to USD）、`CB001`（CA→CA 内部账户转账 FTS）、`CB103`（CA→CA 以外账户转账 FTS）
- **settlement_code**：CMA 账户间互转需要额外配置的标识（如 `CMA3->CMA4`）。
- **核心数据表**：
  - `reconciliation.t_settlement_template`，详见 [[tbl_t_settlement_template]]
  - `reconciliation.t_settlement_detail`，详见 [[tbl_t_settlement_detail]]
