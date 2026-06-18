---
title: 结算类型与产品码映射
domain: manual-fund-settlement
kind: wiki_page
slug: settlement-type-product-code-mapping
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:tester/1107722264
tags: []
---

# 结算类型与产品码映射

人工资金调拨在创建结算模板时需先选定 `settlementType`（代码写死枚举，非配置），不同 `settlementType` 下通过 `biz_product_code` 区分具体的资金调拨场景与目标账户。本页列出两类 `settlementType` 下各产品码的适用场景。

## settlementType 枚举

- `INNER_ACCOUNT`：内部账户结算
- `MERCHANT_ACCOUNT`：商户账户结算

两者均通过 [[tbl_t_settlement_template]] 与 [[tbl_t_settlement_detail]] 落库，详细的资金流向见 [[manual-settlement-fund-flow]]。

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
| `CB001` | CA 向 CA 内部账户转账 |
| `CB103` | CA 向 CA 以外账户转账 |

## 模板账户配置来源

模板中可选的付款方/收款方/银行存款账户在 Reconciliation Manage — Recon Config 中维护：

- Payer List：`SettlementMerchantPayerInfoList`、`SettlementCB103PayerInfoList`、`SettlementCB001PayerInfoList`
- Beneficiary List：`SettlementCB103BeneficiaryInfoList`、`SettlementInnerBeneficiaryInfoList`
- Bank Deposit Account：`SettlementInnerFundOutBankAccountList`

## 相关链接

- 总体流程与背景：[[manual-fund-settlement-overview]]、[[flow_manual-fund-settlement]]
- 各产品码对应的会计分录：[[manual-settlement-fund-flow]]
