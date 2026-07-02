---
id: tbl_reconciliation_t_fund_summary
object_type: Table
name: t_fund_summary (t_fund_summary)
aliases: [t_fund_summary, reconciliation.t_fund_summary]
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

# t_fund_summary (t_fund_summary)

## 用途
物理表 `reconciliation.t_fund_summary`,主键 `summary_id`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `summary_id` | varchar(32) | 汇总id |
| `bank_code` | varchar(15) | Bank Code · 可空 |
| `fund_trans_type` | varchar(30) | Fund Trans Type · 可空 |
| `bill_date` | varchar(8) | 对账日期 · 可空 |
| `status` | varchar(1) | 对账状态,S/P/F · 可空 |
| `summary` | varchar(255) | 汇总备注 · 可空 |
| `outer_cnt` | int(16) | 外部笔数 · 可空 |
| `outer_amount` | decimal(15, 2) | 外部金额 · 可空 |
| `inner_cnt` | int(16) | 内部笔数 · 可空 |
| `inner_amount` | decimal(15, 2) | 内部金额 · 可空 |
| `diff_amount` | decimal(15, 2) | 差异金额 · 可空 |
| `accounting_amount` | decimal(19, 2) | 登账金额 · 可空 |
| `currency` | char(3) | 币种 · 可空 |
| `gmt_create` | timestamp(3) | 创建时间 · 可空 |
| `gmt_modified` | timestamp(3) | 修改时间 · 可空 |

## 主键 / 索引
- 主键:`summary_id`
- 无(仅主键)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
