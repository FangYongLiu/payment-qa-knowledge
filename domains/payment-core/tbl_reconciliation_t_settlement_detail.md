---
id: tbl_reconciliation_t_settlement_detail
object_type: Table
name: 结算明细表(reconciliation.t_settlement_detail)
aliases:
- t_settlement_detail
- reconciliation.t_settlement_detail
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-25'
source_type: wiki
source_ref: confluence:tester/1107722264; wiki:11dc5fef-89b3-45ad-81a8-95bfefa0519a
tags:
- settlement
- reconciliation
- detail
related_services:
- svc_reconciliation
related_scenarios:
- scn_payment_core_manual_fund_settlement
---

# 结算明细表(reconciliation.t_settlement_detail)

## 用途
存储人工资金调拨场景下的**结算申请明细记录**,物理位置 `reconciliation.t_settlement_detail`,归属 [[svc_reconciliation]]。在 counter — settlement detail — apply settlement 流程中,操作员选择已审核通过的结算模板、输入金额、提交审核、审核通过后由系统调拨,相关申请明细落库本表。端到端流程见 [[flow_manual_fund_settlement]]。

## 关联关系
- **所属服务**:[[svc_reconciliation]](= frontmatter `related_services`)
- **谁读写它**:操作入口 [[svc_counter]];申请关联到模板表 [[tbl_reconciliation_t_settlement_template]]。
- **哪些场景校验它**:[[scn_payment_core_manual_fund_settlement]](= `related_scenarios`)。

## 关键列
原文未列出本表物理字段定义(待补)。Settlement Detail 页面展示的业务要素包括:
- 关联的结算模板(来自 `reconciliation.t_settlement_template`)
- 业务类型 / Settlement No / Settlement Type(如 `MANUAL`)
- 结算类型 `settlementType`(代码写死枚举:`INNER_ACCOUNT` / `MERCHANT_ACCOUNT`)
- 业务产品码 `biz_product_code`(500105 / 500108 / 500109 / 500110 / 500111 / 500113 / 230601 / 230602 / CB001 / CB103)
- Voucher、Settlement Amount、Settlement Currency(如 `AED`)、Target Account、Fee Amount、File Url
- Operator、**Audit Status**(如 `PASS`)、**Settlement Result**(`SUCCESS` / `FAIL`)
- Result Code/Msg(失败回填,如 `FTD-06...`)、Memo、Create/Update 时间

## 主键/索引
原文未提供。待补。

## 校验点(QA 关注)
- 申请明细应正确关联到已审核通过的 `t_settlement_template` 模板。
- 明细中的 `settlementType` 与 `biz_product_code` 须符合映射关系(见 [[scn_payment_core_manual_fund_settlement]])。
- CMA 账户间互转的明细需匹配模板中配置的 `settlement_code`(如 `CMA3->CMA4`)。
- 状态流转应在明细记录中体现:提交审核 → Audit Status=PASS → 系统调拨 → Settlement Result=SUCCESS/FAIL(失败时 Result Code/Msg 回填)。
- 审核通过后触发的资金调拨,其 DR/CR 分录应与对应 `biz_product_code` 在 [[scn_payment_core_manual_fund_settlement]] 中定义的资金流一致。
