---
title: 人工资金调拨总览
domain: manual-fund-settlement
kind: wiki_page
slug: manual-fund-settlement-overview
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:tester/1107722264
tags: []
---

# 人工资金调拨总览

为清算团队提供统一的账户结算入口，规范化资金调拨的操作凭证、审核流程与记录。

## 背景

- 业务资金场景日益丰富，清算团队需登录不同 portal 进行资金划拨。
- 存在资金划拨记录不统一、操作复杂、流程不规范等潜在问题。
- 目标：建设统一账户结算入口，统一对资金账户进行结算操作，并规范操作凭证与审核流程。

## 相关需求

- **FAB 0040 AED 账户出款**：Counter settlement function。
- **FAB 0062 USD 账户出款**：0062 美元 H2H 出款及账户登账需求。
- **ENBD CMA AED 账户出款**：ENBD Transfer and Reconciliation；ENBD 二期-余额调节。

## 整体流程

详细步骤参见 [[flow_manual-fund-settlement]]。

1. **创建结算模板**：路径 `counter — settlement management — settlement Template`；选择结算类型 → 填写出款账户信息 → 提交审核 → 审核通过。
2. **发起结算申请**：路径 `counter — settlement detail — apply settlement`；选择模板 → 输入金额 → 提交审核 → 审核通过 → 系统调拨。
3. **系统调拨**：审核通过后由系统按资金流登账，详见 [[manual-settlement-fund-flow]]。

## 结算类型与产品码

`settlementType` 非配置项，代码中写死枚举，主要分两大类：

- `INNER_ACCOUNT`：覆盖备付金体系内/外的内部账户出款，以及 ENBD CMA 账户间互转。
- `MERCHANT_ACCOUNT`：商户出款，包含 AED to AED、AED to USD，以及 CA 内部/外部账户转账。

完整 `settlementType` → `biz_product_code` 映射与适用场景见 [[settlement-type-product-code-mapping]]。

## 配置说明

### CMA 账户互转

CMA 账户间互转需额外配置 `settlement_code`（例如 `CMA3->CMA4`）。

### 模板账户配置（Reconciliation Manage — Recon Config）

- **Payer List**：
  - `SettlementMerchantPayerInfoList`
  - `SettlementCB103PayerInfoList`
  - `SettlementCB001PayerInfoList`
- **Beneficiary List**：
  - `SettlementCB103BeneficiaryInfoList`
  - `SettlementInnerBeneficiaryInfoList`
- **Bank Deposit Account**：
  - `SettlementInnerFundOutBankAccountList`

### 数据库表

- [[tbl_t_settlement_template]]：`reconciliation.t_settlement_template`
- [[tbl_t_settlement_detail]]：`reconciliation.t_settlement_detail`
