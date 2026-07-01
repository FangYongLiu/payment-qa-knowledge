---
id: tbl_reconciliation_t_settlement_template
object_type: Table
name: 结算模板表(reconciliation.t_settlement_template)
aliases:
- t_settlement_template
- reconciliation.t_settlement_template
domain: settlement
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-25'
source_type: wiki
source_ref: confluence:tester/1107722264; wiki:11dc5fef-89b3-45ad-81a8-95bfefa0519a
tags:
- settlement
- reconciliation
- template
related_services:
- svc_reconciliation
related_scenarios:
- scn_payment_core_manual_fund_settlement
---

# 结算模板表(reconciliation.t_settlement_template)

## 用途
存储人工资金调拨场景下的**结算模板配置**,物理位置 `reconciliation.t_settlement_template`,归属 [[svc_reconciliation]]。模板由清算团队在 counter — settlement management — settlement Template 创建,选择结算类型、填写出款账户信息后提交审核;审核通过后用于发起结算申请(counter — settlement detail — apply settlement)。端到端流程见 [[flow_manual_fund_settlement]]。

## 关联关系
- **所属服务**:[[svc_reconciliation]](= frontmatter `related_services`)
- **谁读写它**:操作入口 [[svc_counter]];发起结算申请时关联到明细表 [[tbl_reconciliation_t_settlement_detail]]。
- **哪些场景校验它**:[[scn_payment_core_manual_fund_settlement]](= `related_scenarios`)。

## 关键列
本表对应 "Add Template" 表单字段(`*` 为必填),物理列名以原文为准,部分「待补」:

| 业务字段 | 必填 | 说明 |
| --- | --- | --- |
| SettlementType | * | 结算类型枚举(代码写死,非配置):`INNER_ACCOUNT` / `MERCHANT_ACCOUNT` |
| SettlementCode | | CMA 账户间互转等场景区分具体账户对,如 `CMA3->CMA4` |
| Business Name | * | 结算业务名称 |
| Bank Deposit Account | * | 下拉,来源 `SettlementInnerFundOutBankAccountList` |
| Settlement ProductCode | * | 下拉选择 |
| Biz ProductCode | * | 业务产品码,见 [[scn_payment_core_manual_fund_settlement]] 的映射 |
| Payer AccountNo | * | 付款方账号 |
| Beneficiary List | | 下拉,来源对应 beneficiary 配置列表 |
| Beneficiary Iban/Account | * | 收款方 IBAN/账号 |
| beneficiary SwiftCode | | 收款方 SwiftCode |
| Beneficiary BankName | | 收款方银行名称 |
| Beneficiary AccountName | * | 收款方户名 |
| Beneficiary Address | * | 收款方地址 |
| Beneficiary AccountCurrency | | 收款方账户币种 |
| Attachment | | 附件上传 |
| Memo | | 备注 |

账户配置来源(Reconciliation Manage — Recon Config):
- payer List:`SettlementMerchantPayerInfoList`、`SettlementCB103PayerInfoList`、`SettlementCB001PayerInfoList`
- beneficiary List:`SettlementCB103BeneficiaryInfoList`、`SettlementInnerBeneficiaryInfoList`
- Bank Deposit Account:`SettlementInnerFundOutBankAccountList`

## 主键/索引
原文未提供。待补。

## 校验点(QA 关注)
- `settlementType` 必须命中代码枚举(`INNER_ACCOUNT` / `MERCHANT_ACCOUNT`),不可通过配置新增。
- `settlementType` 与 `biz_product_code` 须符合映射场景(见 [[scn_payment_core_manual_fund_settlement]])。
- CMA 账户间互转模板必须配置 `settlement_code`。
- 模板需经审核通过后才能用于发起结算申请。
- payer / beneficiary / Bank Deposit Account 配置须与 `settlementType` 匹配(如 MERCHANT_ACCOUNT 用 `SettlementMerchantPayerInfoList`;CB103 用对应 payer/beneficiary list;内部账户出款 beneficiary 用 `SettlementInnerBeneficiaryInfoList`;银行扣款账户用 `SettlementInnerFundOutBankAccountList`)。
