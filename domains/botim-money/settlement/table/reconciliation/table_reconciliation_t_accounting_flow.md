---
id: tbl_reconciliation_t_accounting_flow
object_type: Table
name: 登账记录表 (t_accounting_flow)
aliases: [t_accounting_flow, reconciliation.t_accounting_flow]
domain: settlement
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: reconciliation schema DDL
tags: [settlement, reconciliation]
sensitivity: normal
related_services: []
---

# 登账记录表 (t_accounting_flow)

## 用途
物理表 `reconciliation.t_accounting_flow`,主键 `flow_id`。登账记录表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `flow_id` | bigint(17) | 流水ID 主键 |
| `voucher_no` | varchar(64) | 凭证号 · 可空 |
| `voucher_type` | varchar(16) | 凭证类型 · 可空 |
| `voucher_date` | timestamp | 凭证获取时间 · 可空 |
| `dr_account_no` | varchar(32) | dr账户号 · 可空 |
| `dr_member_id` | varchar(32) | dr会员ID · 可空 |
| `dr_fund_type` | varchar(32) | dr资金属性 · 可空 |
| `cr_account_no` | varchar(32) | cr账户号 · 可空 |
| `cr_member_id` | varchar(32) | cr会员ID · 可空 |
| `cr_fund_type` | varchar(32) | cr资金属性 · 可空 |
| `amount` | decimal(15, 2) | 金额 · 可空 |
| `unfreeze_amount` | decimal(15, 2) | 解冻金额 · 可空 |
| `currency` | varchar(3) | 币种 · 可空 |
| `status` | varchar(4) | 状态 · 可空 |
| `message` | varchar(128) | 登账结果 · 可空 |
| `operator` | varchar(64) | 操作人员 · 可空 |
| `memo` | varchar(255) | 备注 · 可空 |
| `bill_memo` | varchar(255) | 账单备注 · 可空 |
| `oss_path` | varchar(255) | 附件文件ossPath · 可空 |
| `accounting_type` | varchar(16) | 登账业务类型 · 可空 |
| `biz_no` | varchar(32) | 关联业务单号 · 可空 |
| `gmt_create` | timestamp | 创建时间 · 可空 |
| `gmt_modified` | timestamp | 更新时间 · 可空 |

## 主键 / 索引
- 主键:`flow_id`
- 无(仅主键)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
