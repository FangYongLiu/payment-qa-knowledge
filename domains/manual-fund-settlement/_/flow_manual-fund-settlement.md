---
id: flow_manual-fund-settlement
object_type: Flow
domain: manual-fund-settlement
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: wiki
source_ref: confluence:tester/1107722264
tags:
- settlement
- counter
- approval
subdomain: null
module: null
sensitivity: normal
name: 人工资金调拨流程
aliases: []
related_services: []
related_tables:
- tbl_t_settlement_template
- tbl_t_settlement_detail
related_scenarios:
- settlement-type-product-code-mapping
- manual-settlement-fund-flow
related_logs: []
related_requirements: []
related_failures: []
---

## 概述
统一的账户结算入口，供清算团队对资金账户进行统一的结算操作，规范化操作凭证与审核流程。端到端流程：创建结算模板 → 审核 → 发起结算申请 → 审核 → 系统调拨完成资金划拨。

## 步骤(跨系统)
1. **创建结算模板**
   - 入口：counter — settlement management — settlement Template
   - 操作：选择结算类型 → 填写相关出款账户信息 → 提交审核 → 审核通过
   - `settlementType` 非配置，代码写死枚举
   - CMA 账户间互转需要配置 `settlement_code`(eg: CMA3->CMA4)
   - 模板中账户配置入口：Reconciliation Manage — Recon Config
     - payer List：SettlementMerchantPayerInfoList、SettlementCB103PayerInfoList、SettlementCB001PayerInfoList
     - beneficiary List：SettlementCB103BeneficiaryInfoList、SettlementInnerBeneficiaryInfoList
     - Bank Deposit Account：SettlementInnerFundOutBankAccountList
   - 落库：reconciliation.t_settlement_template、reconciliation.t_settlement_detail

2. **发起结算申请**
   - 入口：counter — settlement detail — apply settlement
   - 操作：选择模板 → 输入金额 → 提交审核 → 审核通过 → 系统调拨

3. **系统调拨**
   - 审核通过后，系统按所选模板对应的 `settlementType` 与 `biz_product_code` 完成资金划拨记账。

## 涉及服务/表
- 表：`reconciliation.t_settlement_template`、`reconciliation.t_settlement_detail`
- 配置入口：Reconciliation Manage — Recon Config
- 操作入口：counter — settlement management / settlement detail

## 校验点
- `settlementType` 必须为代码内置枚举之一(INNER ACCOUNT、MERCHANT_ACCOUNT 等)，与 `biz_product_code` 匹配适用场景。
- CMA 账户间互转必须配置 `settlement_code`。
- 结算模板与结算申请均需经过提交审核 → 审核通过两道流程，方可触发系统调拨。
- 出款账户信息须通过对应 payer / beneficiary / Bank Deposit Account 列表配置。
