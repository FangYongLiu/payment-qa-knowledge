---
id: tbl_credit_t_cs_order_top_up
object_type: Table
name: Order temp data (t_cs_order_top_up)
aliases: [t_cs_order_top_up, credit.t_cs_order_top_up]
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

# Order temp data (t_cs_order_top_up)

## 用途
物理表 `credit.t_cs_order_top_up`,主键 `id`。Order temp data。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | primary id · 可空 |
| `user_id` | varchar(20) | user member Id |
| `order_no` | varchar(50) | order no |
| `status` | smallint(5) | status |
| `is_read` | smallint(2) | is read |
| `created_time` | timestamp | create time · 可空 |
| `last_modified` | timestamp | last modified time · 可空 |
| `loan_amount` | decimal(15, 2) | loan amount |
| `fee` | decimal(15, 2) | process fee · 可空 |
| `fund_amount` | decimal(15, 2) | fund amount · 可空 |
| `lenders` | varchar(20) | lenders |
| `apply_fund_time` | timestamp | submit fund time · 可空 |
| `period` | smallint (5) | period |
| `period_unit` | smallint(5) |  1 day 2month |
| `product_code` | varchar(10) | product |
| `credit_id` | int | credit id |
| `audit_start_time` | timestamp | 待补 · 可空 |
| `audit_finish_time` | timestamp | 待补 · 可空 |
| `penalty` | int(5) | penalty rate |
| `partner_id` | varchar(20) | channel |
| `source_order_no` | varchar(50) | source order no |
| `ext` | varchar(50) | ext info · 可空 |
| `father_order_no` | varchar(50) | father order no |

## 主键 / 索引
- 主键:`id`
- `idx_father_order_no`:father_order_no
- `idx_idx_created_time`:created_time
- `idx_order_no`:order_no
- `idx_source_order_no`:source_order_no
- `idx_user_id`:user_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
