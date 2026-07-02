---
id: tbl_sme_t_loan_order
object_type: Table
name: Loan order sheet (t_loan_order)
aliases: [t_loan_order, sme.t_loan_order]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: sme schema DDL
tags: [lending, sme]
sensitivity: normal
related_services: []
---

# Loan order sheet (t_loan_order)

## 用途
物理表 `sme.t_loan_order`,主键 `id`。Loan order sheet。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | 待补 · 可空 |
| `order_no` | varchar(64) | Loan application order unique ID |
| `loan_amount` | decimal(15, 2) | Loan amount |
| `currency` | char(3) | currency |
| `status` | smallint | 待补 |
| `user_product_id` | int | The product id used on the user |
| `third_party_product_id` | int | Product id used by the three parties · 可空 |
| `cooling_period` | smallint | Cooling-off period |
| `third_user_id` | varchar(20) | Third-party channel user id |
| `third_order_no` | varchar(64) | Three-party channel order number |
| `third_party_name` | varchar(20) | Order source channel name |
| `create_time` | timestamp | Creation time |
| `update_time` | timestamp | Modification time |

## 主键 / 索引
- 主键:`id`
- `uk_ono`:order_no (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
