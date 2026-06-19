---
title: 结算类型与产品码映射
domain: manual-fund-settlement
kind: wiki_page
slug: settlement-type-product-code-mapping
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki
source_ref: wiki:11dc5fef-89b3-45ad-81a8-95bfefa0519a
tags: []
---

# 结算类型与产品码映射

人工资金调拨在创建结算模板时需先选定 `settlementType`（代码写死枚举，非配置），不同 `settlementType` 下通过 `biz_product_code` 区分具体的资金调拨场景与目标账户。本页列出两类 `settlementType` 下各产品码的适用场景。

## 背景

随着业务资金场景的不断丰富，清算团队此前需登录不同 portal 进行资金划拨，存在记录不统一、操作复杂、流程不规范等问题。统一账户结算入口旨在为清算团队提供统一的资金账户结算操作，并规范化操作凭证与审核流程。整体背景与流程详见 [[manual-fund-settlement-overview]]。

## settlementType 枚举

- `INNER_ACCOUNT`：内部账户结算
- `MERCHANT_ACCOUNT`：商户账户结算

两者均通过 [[tbl_t_settlement_template]] 与 [[tbl_t_settlement_detail]] 落库（库名 `reconciliation`），详细的资金流向见 [[manual-settlement-fund-flow]]。

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

## 相关需求 wiki

- FAB 0040 AED 账户出款：Counter settlement function（4）
- FAB 0062 USD 账户出款：0062 美元 H2H 出款以及账户登账需求
- ENBD CMA AED 账户出款：14.4 ENBD Transfer and Reconciliation；ENBD 二期-余额调节

## 操作流程概览

1. **创建结算模板**：Counter — Settlement Management — Settlement Template。选择结算类型 → 填写相关出款账户信息 → 提交审核 → 审核通过。模板配置细节参见 [[settlement-template-config]]。
2. **发起结算申请**：Counter — Settlement Detail — Apply Settlement。选择模板 → 输入金额 → 提交审核 → 审核通过 → 系统调拨。
3. **资金流转**：按 `biz_product_code` 触发对应的会计分录，参见 [[manual-settlement-fund-flow]] 与 [[flow_manual_fund_settlement]]。

## 模板账户配置来源

模板中可选的付款方/收款方/银行存款账户在 Reconciliation Manage — Recon Config 中维护：

- Payer List：`SettlementMerchantPayerInfoList`、`SettlementCB103PayerInfoList`、`SettlementCB001PayerInfoList`
- Beneficiary List：`SettlementCB103BeneficiaryInfoList`、`SettlementInnerBeneficiaryInfoList`
- Bank Deposit Account：`SettlementInnerFundOutBankAccountList`

## 相关链接

- 总体流程与背景：[[manual-fund-settlement-overview]]、[[flow_manual_fund_settlement]]
- 模板配置说明：[[settlement-template-config]]
- 各产品码对应的会计分录：[[manual-settlement-fund-flow]]
- 落库表：[[tbl_t_settlement_template]]、[[tbl_t_settlement_detail]]
