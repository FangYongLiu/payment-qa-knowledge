---
id: tbl_credit_t_cs_transfer_record
object_type: Table
name: transfer record (t_cs_transfer_record)
aliases: [t_cs_transfer_record, credit.t_cs_transfer_record]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: credit schema DDL
tags: [lending, credit]
sensitivity: normal
related_services: []
---

# transfer record (t_cs_transfer_record)

## 用途
物理表 `credit.t_cs_transfer_record`,主键 `id`。transfer record。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int(11) | id · 可空 |
| `created_time` | timestamp | create time |
| `last_modified` | timestamp | update time |
| `status` | tinyint(5) | -1:fail 0:init 1:success |
| `type` | tinyint(5) | 1:buyback |
| `source_order_no` | varchar(64) | old order no |
| `new_order_no` | varchar(64) | new order no |
| `payment_account` | varchar(30) | payment account |
| `receive_account` | varchar(30) | receive account |
| `amount` | decimal(15, 2) | transfer amount |
| `payment_time` | timestamp | payment time · 可空 |
| `payment_no` | varchar(64) | payment no · 可空 |
| `transfer_no` | varchar(32) | pay sys product orderNo · 可空 |
| `settle_time` | timestamp | settle success event time · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_new_order_no`:new_order_no
- `idx_payment_no`:payment_no
- `idx_source_order_no`:source_order_no

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
