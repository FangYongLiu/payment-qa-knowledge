---
id: flow_manual_fund_settlement
object_type: Flow
domain: manual-fund-settlement
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: wiki
source_ref: wiki:55ce713d-d31a-4ab2-83c9-3361843358f6
tags:
- counter
- settlement
- 结算
subdomain: null
module: null
sensitivity: normal
name: 人工资金调拨端到端流程
aliases: []
related_services: []
related_tables:
- reconciliation.t_settlement_template
- reconciliation.t_settlement_detail
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 概述
清算团队通过统一账户结算入口（counter）对资金账户进行结算操作，覆盖创建结算模板 → 发起结算申请 → 审核 → 系统调拨的完整业务流，并实现操作凭证与审核流程的规范化记录。适用场景包括 FAB 0040 AED 账户出款、FAB 0062 USD 账户出款、ENBD CMA AED 账户出款及 CMA 账户间互转等。

## 步骤(跨系统)
### 1. 创建结算模板
路径：counter — settlement management — settlement Template
- 选择 settlementType（代码写死枚举，非配置）
- 填写相关出款账户信息
- 提交审核 → 审核通过

settlementType 与 biz_product_code 对应关系：
- INNER ACCOUNT
  - 500105：出备付金体系内部账户出款（FAB 0040 AED、FAB 0062 USD 至本行/他行 IBAN，FAB219/FAB220/FAB223）
  - 500108：不出备付金体系内部账户出款（payby 内部资金调用，FAB 0040 AED → ENBD CMA、FAB 0062 USD → ENBD CMA）
  - 500109：ENBD CMA3 AED → FAB 0040 AED（ENBD210）
  - 500110：ENBD CMA3 AED → ENBD CMA2 / CMA4 AED（ENBD209）
  - 500111：ENBD CMA2 AED → ENBD CMA3 AED（ENBD204）
  - 500113：ENBD CMA4 AED → ENBD CMA3 AED（ENBD201）
- MERCHANT_ACCOUNT（商户出款）
  - 230601：AED to AED
  - 230602：AED to USD
  - CB001：CA 向 CA 内部账户转账
  - CB103：CA 向 CA 以外账户转账

CMA 账户间互转需配置 settlement_code（eg: CMA3->CMA4）。

模版账户配置（Reconciliation Manage — Recon Config）：
- payer List：SettlementMerchantPayerInfoList、SettlementCB103PayerInfoList、SettlementCB001PayerInfoList
- beneficiary List：SettlementCB103BeneficiaryInfoList、SettlementInnerBeneficiaryInfoList
- Bank Deposit Account：SettlementInnerFundOutBankAccountList

### 2. 发起结算申请
路径：counter — settlement detail — apply settlement
- 选择模板 → 输入金额 → 提交审核 → 审核通过 → 系统调拨

### 3. 系统调拨（资金流）
0042 出款：
- DR：78429990020010001 / CR：78429990030010002
- DR：78429990030010002 / CR：78430030020010002

0062 出款：
- DR：84040030020010001 USD capital reserve-FAB-0062 100 USD / CR：84029990030010002 Other Accounts Payable - Pending check for settlement - 0062 USD
- DR：84029990030010002 / CR：84040010010010001 FundOut Pending for Clearing-FAB-H2H-0062 USD

CMA 出款：
- 500111（CMA2 → CMA3）：DR 78430010210010003 FundIn Pending for Clearing-ENBD CMA3 / CR 78430030040020001 FundOut Pending for Clearing-CMA2-ENBD204
- 500113（CMA4 → CMA3）：DR 78430010210010003 FundIn Pending for Clearing-ENBD CMA3 / CR 78430030040040001 FundOut Pending for Clearing-CMA2-ENBD201
- 500110（CMA3 → CMA2）：DR 78430010210010002 FundIn Pending for Clearing-ENBD CMA2 / CR 78430030040030001 FundOut Pending for Clearing-CMA3-ENBD209
- 500110（CMA3 → CMA4）：DR 78430010210010004 FundIn Pending for Clearing-ENBD CMA4 / CR 78430030040030001 FundOut Pending for Clearing-CMA3-ENBD210

## 涉及服务/表
- 数据库：reconciliation.t_settlement_template、reconciliation.t_settlement_detail
- 配置入口：Reconciliation Manage — Recon Config
- 操作入口：counter（settlement management / settlement detail）

## 校验点
- settlementType 为代码写死枚举，不可通过配置新增
- 模板提交后必须经过审核通过才能使用
- 结算申请提交后必须经过审核通过，方可触发系统调拨
- CMA 账户间互转需正确配置 settlement_code（如 CMA3->CMA4）
- 模板内 payer / beneficiary / Bank Deposit Account 需在 Recon Config 中正确维护对应清单
- settlementType 与 biz_product_code 必须匹配适用场景（如 500105 为出备付金体系内部账户出款，500108 为不出备付金体系）
