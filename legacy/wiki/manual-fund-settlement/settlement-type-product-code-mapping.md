---
title: 结算类型与产品码映射
domain: manual-fund-settlement
kind: wiki_page
slug: settlement-type-product-code-mapping
status: archived
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:AQ/1138425935
tags: []
---

# 结算类型与产品码映射

人工资金调拨在创建结算模板时需先选定 `settlementType`（代码写死枚举，非配置），不同 `settlementType` 下通过 `biz_product_code` 区分具体的资金调拨场景与目标账户。本页列出两类 `settlementType` 下各产品码的适用场景。

## 背景

随着业务资金场景的不断丰富，清算团队需要登录到不同的 portal 进行资金划拨工作，带来了资金划拨记录不统一、操作复杂、流程不规范等问题。统一账户结算入口建设后，清算团队可在同一处对资金账户进行结算操作，并实现操作凭证、审核流程的规范化记录。

涉及的资金场景需求来源：

- FAB 0040 AED 账户出款：Counter settlement function
- FAB 0062 USD 账户出款：0062 美元 H2H 出款以及账户登账需求
- ENBD CMA AED 账户出款：14.4 ENBD Transfer and Reconciliation、ENBD 二期 — 余额调节

## settlementType 枚举

- `INNER_ACCOUNT`：内部账户结算
- `MERCHANT_ACCOUNT`：商户账户结算

两者均通过 `reconciliation.t_settlement_template` 与 `reconciliation.t_settlement_detail` 落库，详细的资金流向见 [[settlement-fund-flow]]。

## 创建与发起流程

1. **创建结算模板**（Counter — Settlement Management — Settlement Template）：选择结算类型 → 填写相关出款账户信息 → 提交审核 → 审核通过。`settlementType` 非配置，代码写死枚举。
2. **发起结算申请**（Counter — Settlement Detail — Apply Settlement）：选择模板 → 输入金额 → 提交审核 → 审核通过 → 系统调拨。

模板配置细节见 [[settlement-template-config]]。

## INNER_ACCOUNT 产品码

| biz_product_code | 适用场景 |
| --- | --- |
| `500105` | 出备付金体系的内部账户出款。包含 FAB 0040 AED 账户出款、FAB 0062 USD 账户出款（目标对象为本行或他行 IBAN，对应 FAB219、FAB220、FAB223） |
| `500108` | 不出备付金体系的内部账户出款（payby 内部资金调用）。FAB 0040 AED 账户 → ENBD CMA 账户；FAB 0062 USD 账户 → ENBD CMA 账户 |
| `500109` | ENBD CMA3 AED 账户 → FAB 0040 AED 账户（ENBD210） |
| `500110` | ENBD CMA3 AED 账户 → ENBD CMA2 / CMA4 AED 账户（ENBD209） |
| `500111` | ENBD CMA2 AED 账户 → ENBD CMA3 AED 账户（ENBD204） |
| `500113` | ENBD CMA4 AED 账户 → ENBD CMA3 AED 账户（ENBD201） |

> CMA 账户间互转还需额外配置 `settlement_code`（如 `CMA3->CMA4`）以区分具体路由。

## MERCHANT_ACCOUNT 产品码

用于商户出款场景：

| biz_product_code | 适用场景 |
| --- | --- |
| `230601` | AED to AED |
| `230602` | AED to USD |
| `CB001` | CA 向 CA 内部账户转账（FTS） |
| `CB103` | CA 向 CA 以外账户转账（FTS） |

## 模板账户配置来源

模板中可选的付款方/收款方/银行存款账户在 Reconciliation Manage — Recon Config 中维护：

- **Payer List**：`SettlementMerchantPayerInfoList`、`SettlementCB103PayerInfoList`、`SettlementCB001PayerInfoList`
- **Beneficiary List**：`SettlementCB103BeneficiaryInfoList`、`SettlementInnerBeneficiaryInfoList`
- **Bank Deposit Account**：`SettlementInnerFundOutBankAccountList`

## 资金流（产品码对应分录）

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

### CMA 出款

- **500111（CMA2 → CMA3）**
  - DR：FundIn Pending for Clearing - ENBD CMA3（`78430010210010003`）
  - CR：FundOut Pending for Clearing - CMA2 - ENBD204（`78430030040020001`）
- **500113（CMA4 → CMA3）**
  - DR：FundIn Pending for Clearing - ENBD CMA3（`78430010210010003`）
  - CR：FundOut Pending for Clearing - CMA2 - ENBD201（`78430030040040001`）
- **500110（CMA3 → CMA2）**
  - DR：FundIn Pending for Clearing - ENBD CMA2（`78430010210010002`）
  - CR：FundOut Pending for Clearing - CMA3 - ENBD209（`78430030040030001`）
- **500110（CMA3 → CMA4）**
  - DR：FundIn Pending for Clearing - ENBD CMA4（`78430010210010004`）
  - CR：FundOut Pending for Clearing - CMA3 - ENBD210（`78430030040030001`）

## 相关链接

- 总体流程与背景：[[manual-fund-settlement-overview]]
- 模板配置说明：[[settlement-template-config]]
- 各产品码对应的完整账务流水：[[settlement-fund-flow]]
