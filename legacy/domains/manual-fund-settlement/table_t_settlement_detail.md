---
id: tbl_t_settlement_detail
object_type: Table
domain: manual-fund-settlement
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-19'
source_type: wiki
source_ref: wiki:11dc5fef-89b3-45ad-81a8-95bfefa0519a
tags:
- settlement
- detail
subdomain: null
module: null
sensitivity: normal
name: 结算明细表
aliases:
- reconciliation.t_settlement_detail
related_services: []
related_tables:
- tbl_t_settlement_template
related_scenarios:
- manual-settlement-fund-flow
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
存储人工资金调拨场景下的结算申请明细记录。在 counter — settlement detail — apply settlement 流程中，操作员选择结算模板、输入金额、提交审核、审核通过后由系统调拨，相关申请明细落库于 reconciliation.t_settlement_detail。

## 关键列
原文未列出本表字段定义。可关联的业务要素包括：
- 关联的结算模板（来自 reconciliation.t_settlement_template）
- 结算类型 settlementType（代码写死枚举：INNER ACCOUNT / MERCHANT_ACCOUNT）
- 业务产品码 biz_product_code（500105 / 500108 / 500109 / 500110 / 500111 / 500113 / 230601 / 230602 / CB001 / CB103）
- 结算金额（apply settlement 时输入）
- 审核状态（提交审核 → 审核通过 → 系统调拨）

## 主键/索引
原文未提供主键/索引定义。

## 校验点(QA 关注)
- 申请明细应正确关联到已审核通过的 t_settlement_template 模板。
- 申请明细中的 settlementType 与 biz_product_code 须符合「结算类型与产品码映射」中的对应关系。
- CMA 账户间互转的明细需匹配模板中配置的 settlement_code（如 CMA3->CMA4）。
- 申请流程中的状态流转：提交审核 → 审核通过 → 系统调拨，应在明细记录中体现。
- 审核通过后触发的资金调拨，其资金流方向（DR/CR 科目）应与对应 biz_product_code 在 [[manual-settlement-fund-flow]] 中定义的一致。
