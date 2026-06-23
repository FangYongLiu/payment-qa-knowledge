---
title: 结算模板配置说明
domain: manual-fund-settlement
kind: wiki_page
slug: settlement-template-config
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:e8a166c7-9687-411d-9304-7f6c244b4a9c
tags: []
---

# 结算模板配置说明

本页说明人工资金调拨场景下结算模板的创建流程、`settlementType` 枚举与产品码的映射关系，以及账户配置项与底层数据表。模板创建是发起结算申请的前置步骤，详见 [[flow_manual_fund_settlement]]。

## 模板创建流程

入口：counter — settlement management — settlement Template

步骤：
1. 选择结算类型（settlementType）
2. 填写相关出款账户信息
3. 提交审核
4. 审核通过后模板生效

注意：`settlementType` 非配置项，代码中写死为枚举。

## Add Template 表单字段

模板新建弹窗 "Add Template" 包含以下字段（`*` 为必填）：

| 字段 | 必填 | 说明 |
|---|---|---|
| SettlementType | * | 结算类型枚举，如 `INNER_ACCOUNT`、`MERCHANT_ACCOUNT` |
| SettlementCode | | CMA 账户间互转等场景下用于区分具体账户对，例如 `CMA3->CMA4` |
| Business Name | * | 结算业务名称 |
| Bank Deposit Account | * | 下拉选择，来源于 `SettlementInnerFundOutBankAccountList` |
| Settlement ProductCode | * | 下拉选择 |
| Biz ProductCode | * | 业务产品码，见下文枚举映射 |
| Payer AccountNo | * | 付款方账号 |
| Beneficiary List | | 下拉选择，来源于对应的 beneficiary 配置列表 |
| Beneficiary Iban/Account | * | 收款方 IBAN/账号 |
| beneficiary SwiftCode | | 收款方 SwiftCode |
| Beneficiary BankName | | 收款方银行名称 |
| Beneficiary AccountName | * | 收款方户名 |
| Beneficiary Address | * | 收款方地址 |
| Beneficiary AccountCurrency | | 收款方账户币种 |
| Attachment | | 附件上传 |
| Memo | | 备注 |

提交后进入审核流程，审核通过后模板生效。

## settlementType 枚举与产品码映射

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
| CB001 | CA 向 CA 内部账户转账 |
| CB103 | CA 向 CA 以外账户转账 |

### CMA 账户间互转

需要额外配置 `SettlementCode`，例如 `CMA3->CMA4`，用于区分具体的 CMA 账户对。

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

## 相关数据表

- `reconciliation.t_settlement_template`：结算模板主表
- `reconciliation.t_settlement_detail`：结算明细

## 关联

- 模板创建完成后，由清算团队基于模板发起结算申请，参见 [[flow_manual_fund_settlement]]
- 各 settlementType 对应的具体借贷分录见 [[settlement-fund-flow]]
- 整体业务背景见 [[manual-fund-settlement-overview]]
