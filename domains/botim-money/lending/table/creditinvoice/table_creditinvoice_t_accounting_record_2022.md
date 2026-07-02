---
id: tbl_creditinvoice_t_accounting_record_2022
object_type: Table
name: accounting record table (t_accounting_record_2022)
aliases: [t_accounting_record_2022, creditinvoice.t_accounting_record_2022]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: creditinvoice schema DDL
tags: [lending, creditinvoice]
sensitivity: normal
related_services: []
---

# accounting record table (t_accounting_record_2022)

## 用途
物理表 `creditinvoice.t_accounting_record_2022`,主键 `id`。accounting record table。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | 待补 · 可空 |
| `product_code` | varchar(32) | 待补 |
| `busi_entity_no` | varchar(32) | entity no,generally is loan order no |
| `ref_busi_no` | varchar(32) | busi key |
| `busi_time` | timestamp | busi time |
| `scenario` | varchar(16) | scenario |
| `debit_entry_id` | int | debit account id，ref to the id in accounting_entry |
| `debit_amount` | decimal(15, 4) | debit amount |
| `credit_entry_id` | int | credit account id ,ref to the id in accounting_entry |
| `credit_amount` | decimal(15, 4) | credit amount |
| `create_time` | timestamp | 待补 |

## 主键 / 索引
- 主键:`id`
- `uk_d`:busi_entity_no, ref_busi_no, scenario, debit_entry_id, credit_entry_id (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
