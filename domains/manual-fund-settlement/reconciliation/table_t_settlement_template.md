---
id: tbl_t_settlement_template
object_type: Table
domain: manual-fund-settlement
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-19'
source_type: wiki
source_ref: wiki:11dc5fef-89b3-45ad-81a8-95bfefa0519a
tags:
- reconciliation
- settlement
- template
subdomain: reconciliation
module: null
sensitivity: normal
name: 结算模板表
aliases:
- t_settlement_template
related_services: []
related_tables:
- tbl_t_settlement_detail
related_scenarios:
- settlement-template-config
- settlement-type-product-code-mapping
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
存储结算模板配置信息，物理位置 `reconciliation.t_settlement_template`。模板由清算团队在 counter — settlement management — settlement Template 创建，选择结算类型、填写出款账户信息后提交审核，审核通过后可用于发起结算申请（counter — settlement detail — apply settlement）。

## 关键列
- `settlementType`：结算类型，非配置，代码写死枚举。可选值：
  - `INNER_ACCOUNT`：内部账户结算，对应 biz_product_code 500105 / 500108 / 500109 / 500110 / 500111 / 500113
  - `MERCHANT_ACCOUNT`：商户出款，对应 biz_product_code 230601（AED to AED） / 230602（AED to USD） / CB001（CA 向 CA 内部账户转账 FTS） / CB103（CA 向 CA 以外账户转账 FTS）
- `settlement_code`：CMA 账户间互转场景下必须配置，例如 `CMA3->CMA4`。
- 出款账户信息：来自 Reconciliation Manage — Recon Config 配置：
  - payer List：`SettlementMerchantPayerInfoList`、`SettlementCB103PayerInfoList`、`SettlementCB001PayerInfoList`
  - beneficiary List：`SettlementCB103BeneficiaryInfoList`、`SettlementInnerBeneficiaryInfoList`
  - Bank Deposit Account：`SettlementInnerFundOutBankAccountList`

## 主键/索引
原文未提供。

## 校验点(QA 关注)
- `settlementType` 必须命中代码枚举（INNER_ACCOUNT / MERCHANT_ACCOUNT），不可通过配置新增。
- `settlementType` 与 `biz_product_code` 的映射关系需符合定义场景（参见 [[settlement-type-product-code-mapping]]）：
  - 500105：出备付金体系内部账户出款（FAB 0040/0062 IBAN 出款，FAB219/220/223）
  - 500108：不出备付金体系的内部账户出款（FAB → ENBD CMA）
  - 500109：ENBD CMA3 → FAB 0040（ENBD210）
  - 500110：ENBD CMA3 → CMA2/CMA4（ENBD209）
  - 500111：ENBD CMA2 → CMA3（ENBD204）
  - 500113：ENBD CMA4 → CMA3（ENBD201）
- CMA 账户间互转模板必须配置 `settlement_code`。
- 模板需经审核通过后才能用于发起结算申请。
- payer / beneficiary / Bank Deposit Account 配置需与 `settlementType` 相匹配（如 MERCHANT_ACCOUNT 用 SettlementMerchantPayerInfoList，CB103 用对应 payer/beneficiary list，内部账户出款 beneficiary 用 SettlementInnerBeneficiaryInfoList，银行扣款账户用 SettlementInnerFundOutBankAccountList）。
