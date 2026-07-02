---
id: tbl_creditinvoice_t_accounting_record
object_type: Table
name: 会计账目表 (t_accounting_record)
aliases: [t_accounting_record, creditinvoice.t_accounting_record]
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

# 会计账目表 (t_accounting_record)

## 用途
物理表 `creditinvoice.t_accounting_record`,主键 `id`。会计账目表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | 待补 · 可空 |
| `product_code` | varchar(64) | 待补 |
| `busi_entity_no` | varchar(64) | 交易所属主体号：一般是借款单号 |
| `ref_busi_no` | varchar(64) | 交易对应的业务端主键 |
| `busi_time` | timestamp | 业务发生的时间 |
| `scenario` | varchar(32) | 交易所属场景 |
| `debit_entry_id` | int | debit项的科目id，对应accounting_entry表的id |
| `debit_amount` | decimal(15, 4) | Debit项记录的金额 |
| `credit_entry_id` | int | Credit项的科目id，对应accounting_entry表的id |
| `credit_amount` | decimal(15, 4) | credit项金额 |
| `create_time` | timestamp | 待补 |

## 主键 / 索引
- 主键:`id`
- `uk_d`:busi_entity_no, ref_busi_no, scenario, debit_entry_id, credit_entry_id (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
