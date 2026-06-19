---
title: 结算模板配置说明
domain: manual-fund-settlement
kind: wiki_page
slug: settlement-template-config
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki
source_ref: wiki:11dc5fef-89b3-45ad-81a8-95bfefa0519a
tags: []
---

# 结算模板配置说明

本页说明人工资金调拨场景下结算模板的创建流程、`settlementType` 枚举与产品码的映射关系，以及账户配置项与底层数据表。模板创建是发起结算申请的前置步骤，详见 [[flow_manual_fund_settlement]]。

## 背景

随着业务资金场景的不断丰富，清算团队需要登录到不同的 portal 进行资金划拨工作，带来了资金划拨记录不统一、操作复杂、流程不规范等潜在问题。为此建设统一的账户结算入口，供清算团队对资金账户进行统一的结算操作，并实现操作凭证、审核流程的规范化记录。整体业务背景见 [[manual-fund-settlement-overview]]。

## 相关需求场景

- **FAB 0040 AED 账户出款**：Counter settlement function
- **FAB 0062 USD 账户出款**：0062 美元 H2H 出款以及账户登账需求
- **ENBD CMA AED 账户出款**：ENBD Transfer and Reconciliation（14.4）、ENBD 二期 - 余额调节

## 模板创建流程

入口：counter — settlement management — settlement Template

步骤：
1. 选择结算类型（settlementType）
2. 填写相关出款账户信息
3. 提交审核
4. 审核通过后模板生效

注意：`settlementType` 非配置项，代码中写死为枚举。

## settlementType 枚举与产品码映射

完整映射另见 [[settlement-type-product-code-mapping]]。

### INNER ACCOUNT（内部账户出款）

| biz_product_code | 适用场景 |
|---|---|
| 500105 | 出备付金体系的内部账户出款；FAB 0040 AED / FAB 0062 USD 账户出款（目标为本行或他行 IBAN，FAB219、FAB220、FAB223） |
| 500108 | 不出备付金体系的内部账户出款（payby 内部资金调拨）；FAB 0040 AED → ENBD CMA、FAB 0062 USD → ENBD CMA |
| 500109 | ENBD CMA3 AED → FAB 0040 AED（ENBD210） |
| 500110 | ENBD CMA3 AED → ENBD CMA2 / CMA4 AED（ENBD209） |
| 500111 | ENBD CMA2 AED → ENBD CMA3 AED（ENBD204） |
| 500113 | ENBD CMA4 AED → ENBD CMA3 AED（ENBD201） |

### MERCHANT_ACCOUNT（商户出款）

| biz_product_code | 适用场景 |
|---|---|
| 230601 | AED to AED |
| 230602 | AED to USD |
| CB001 | CA 向 CA 内部账户转账（FTS） |
| CB103 | CA 向 CA 以外账户转账（FTS） |

### CMA 账户间互转

需要额外配置 `settlement_code`，例如 `CMA3->CMA4`，用于区分具体的 CMA 账户对。

## 模板中的账户配置项

配置入口：Reconciliation Manage — Recon Config

- **payer List**
  - `SettlementMerchantPayerInfoList`
  - `SettlementCB103PayerInfoList`
  - `SettlementCB001PayerInfoList`
- **beneficiary List**
  - `SettlementCB103BeneficiaryInfoList`
  - `SettlementInnerBeneficiaryInfoList`
- **Bank Deposit Account**
  - `SettlementInnerFundOutBankAccountList`

## 发起结算申请

入口：counter — settlement detail — apply settlement

步骤：选择模板 → 输入金额 → 提交审核 → 审核通过 → 系统调拨

## 资金流

各 settlementType 对应的借贷分录详见 [[manual-settlement-fund-flow]]，下面列举关键账户路径。

### FAB 0040 AED 出款

- DR：`78429990020010001`
- CR：`78429990030010002`
- DR：`78429990030010002`
- CR：`78430030020010002`

### FAB 0062 USD 出款

- DR：`84040030020010001` USD capital reserve - FAB - 0062 100 USD
- CR：`84029990030010002` Other Accounts Payable - Pending check for settlement - 0062 USD
- DR：`84029990030010002` Other Accounts Payable - Pending check for settlement - 0062 USD
- CR：`84040010010010001` FundOut Pending for Clearing - FAB - H2H - 0062 USD

### CMA 账户间互转

| 产品码 | 方向 | DR | CR |
|---|---|---|---|
| 500111 | CMA2 → CMA3 | FundIn Pending for Clearing - ENBD CMA3（`78430010210010003`） | FundOut Pending for Clearing - CMA2 - ENBD204（`78430030040020001`） |
| 500113 | CMA4 → CMA3 | FundIn Pending for Clearing - ENBD CMA3（`78430010210010003`） | FundOut Pending for Clearing - CMA2 - ENBD201（`78430030040040001`） |
| 500110 | CMA3 → CMA2 | FundIn Pending for Clearing - ENBD CMA2（`78430010210010002`） | FundOut Pending for Clearing - CMA3 - ENBD209（`78430030040030001`） |
| 500110 | CMA3 → CMA4 | FundIn Pending for Clearing - ENBD CMA4（`78430010210010004`） | FundOut Pending for Clearing - CMA3 - ENBD210（`78430030040030001`） |

## 相关数据表

- `reconciliation.t_settlement_template`：结算模板主表，参见 [[tbl_t_settlement_template]]
- `reconciliation.t_settlement_detail`：结算明细，参见 [[tbl_t_settlement_detail]]

## 关联

- 模板创建完成后，由清算团队基于模板发起结算申请，参见 [[flow_manual_fund_settlement]]
- 各 settlementType 对应的具体借贷分录见 [[manual-settlement-fund-flow]]
- 整体业务背景见 [[manual-fund-settlement-overview]]
