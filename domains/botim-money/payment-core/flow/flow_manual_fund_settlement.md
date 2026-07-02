---
id: flow_manual_fund_settlement
object_type: Flow
name: 人工资金调拨端到端流程
aliases:
- manual-fund-settlement
- 统一账户结算
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-25'
source_type: wiki
source_ref: confluence:tester/1107722264; wiki:11dc5fef-89b3-45ad-81a8-95bfefa0519a
tags:
- settlement
- counter
- fund-transfer
- approval
related_services:
- svc_counter
- svc_reconciliation
related_tables:
- tbl_reconciliation_t_settlement_template
- tbl_reconciliation_t_settlement_detail
related_scenarios:
- scn_payment_core_manual_fund_settlement
---

# 人工资金调拨端到端流程

## 概述
人工资金调拨为清算团队提供**统一的账户结算入口**，覆盖「创建结算模板 → 审核 → 发起结算申请 → 审核 → 系统调拨」的完整业务流，并规范化操作凭证与审批记录。

建设背景:业务资金场景日益丰富,清算团队此前需登录多个 portal 完成资金划拨,存在记录不统一、操作复杂、流程不规范的问题。统一入口由 [[svc_counter]] 提供操作界面、[[svc_reconciliation]] 提供模板/配置与登账能力。

适用的资金场景(需求来源):
- **FAB 0040 AED 账户出款**:Counter settlement function
- **FAB 0062 USD 账户出款**:0062 美元 H2H 出款及账户登账需求
- **ENBD CMA AED 账户出款**:ENBD Transfer and Reconciliation、ENBD 二期-余额调节(含 CMA 账户间互转)

## 步骤(跨系统)

### 1. 创建结算模板
入口:counter — settlement management — settlement Template
1. 选择结算类型 `settlementType`(代码写死枚举,非配置项)
2. 填写相关出款账户信息(Add Template 表单,字段见 [[tbl_reconciliation_t_settlement_template]])
3. 提交审核 → 审核通过后模板生效

CMA 账户间互转需额外配置 `settlement_code`(如 `CMA3->CMA4`)以区分具体账户对。

模板内账户配置入口:Reconciliation Manage — Recon Config
- payer List:`SettlementMerchantPayerInfoList`、`SettlementCB103PayerInfoList`、`SettlementCB001PayerInfoList`
- beneficiary List:`SettlementCB103BeneficiaryInfoList`、`SettlementInnerBeneficiaryInfoList`
- Bank Deposit Account:`SettlementInnerFundOutBankAccountList`

落库:`reconciliation.t_settlement_template`([[tbl_reconciliation_t_settlement_template]])。

### 2. 发起结算申请
入口:counter — settlement detail — apply settlement
1. 选择已审核通过的模板 → 输入金额 → 提交审核 → 审核通过 → 系统调拨

Settlement Detail 页面能力:按业务类型(如 `CA向CA内部`)、`Status`、时间范围检索结算记录;点击 **Apply Settlement** 发起新申请。结算记录核心字段:业务类型 / Settlement No / Settlement Type(如 `MANUAL`) / Voucher / Settlement Amount / Settlement Currency(如 `AED`) / Target Account / Fee Amount / File Url / Operator / **Audit Status**(如 `PASS`) / **Settlement Result**(`SUCCESS` / `FAIL`) / Result Code/Msg(失败回填,如 `FTD-06...`) / Memo / Create/Update 时间;Action 支持 `Update Status`。

落库:`reconciliation.t_settlement_detail`([[tbl_reconciliation_t_settlement_detail]])。

### 3. 系统调拨(资金流登账)
审核通过后,系统按所选模板的 `settlementType` 与 `biz_product_code` 完成资金划拨记账(DR/CR 分录)。各产品码对应的具体借贷分录与校验见 [[scn_payment_core_manual_fund_settlement]]。

## 关联关系
- **经过的服务(有序)**:[[svc_counter]](操作入口) → [[svc_reconciliation]](模板/配置/登账)(= `related_services`)
- **关键表**:[[tbl_reconciliation_t_settlement_template]]、[[tbl_reconciliation_t_settlement_detail]](= `related_tables`)
- **关键场景**:[[scn_payment_core_manual_fund_settlement]](= `related_scenarios`)
- **下游依赖(待补)**:原 wiki 架构图显示 cmp webservice 下 `settlement` 顶层服务依赖 merchant、ufs、counter、pbs、statement、ma 六个下游组件。其中 counter=[[svc_counter]]、pbs=[[svc_pbs]]、ufs 对应 [[svc_ufs2]];merchant / statement / ma 的对应服务对象「待补」。

## 校验点
- `settlementType` 为代码写死枚举,不可通过配置新增;须与 `biz_product_code` 匹配适用场景。
- 模板提交后必须审核通过才能使用;结算申请提交后必须审核通过方可触发系统调拨。
- CMA 账户间互转必须正确配置 `settlement_code`(如 `CMA3->CMA4`)。
- 模板内 payer / beneficiary / Bank Deposit Account 须在 Recon Config 中维护对应清单,且与 `settlementType` 匹配。
- 系统调拨产生的 DR/CR 分录须与对应 `biz_product_code` 在 [[scn_payment_core_manual_fund_settlement]] 中定义的资金流一致。
