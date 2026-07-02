---
id: tbl_rnpl_t_loan_order
object_type: Table
name: Advance Order Table (t_loan_order)
aliases: [t_loan_order, rnpl.t_loan_order]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: rnpl schema DDL
tags: [lending, rnpl]
sensitivity: normal
related_services: []
---

# Advance Order Table (t_loan_order)

## 用途
物理表 `rnpl.t_loan_order`,主键 `id`。Advance Order Table。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | primary key · 可空 |
| `order_no` | varchar(64) | unique id for Borrowing Request Order |
| `user_id` | varchar(20) | user id |
| `loan_amount` | decimal(15, 2) | loan amount |
| `currency` | char(3) | currency |
| `status` | smallint(4) | status, 0:to be valid 1: to be paid ,2: settled,1: canceled |
| `loan_product_id` | int | Loan product id |
| `tprp_id` | int | Tprp id |
| `due_disburse_time` | timestamp | Due disburse time · 可空 |
| `actual_disburse_time` | timestamp | Actual disburse time · 可空 |
| `finish_repay_time` | timestamp | Finish repay time · 可空 |
| `processing_fee` | decimal(10, 2) | Processing fee |
| `total_interest_fee` | decimal(15, 2) | Total interest fee |
| `contract_id` | int | contract ID, corresponding to the ID field of the t_rent_contract table |
| `cooling_period` | smallint | cooling period\n1：use \n0：waive |
| `create_time` | timestamp | create time |
| `update_time` | timestamp | update time |

## 主键 / 索引
- 主键:`id`
- `uk_ono`:order_no (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
