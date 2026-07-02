---
id: tbl_rnpl_t_bill
object_type: Table
name: Bill Table (t_bill)
aliases: [t_bill, rnpl.t_bill]
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

# Bill Table (t_bill)

## 用途
物理表 `rnpl.t_bill`,主键 `id`。Bill Table。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | primary key · 可空 |
| `status` | int | Status: 1: pending; 2 cleared; -1: canceled (overdue first bill order canceled) |
| `period_num` | int | period number |
| `due_time` | timestamp | repayment due date · 可空 |
| `finish_repay_time` | timestamp | completion date · 可空 |
| `user_id` | varchar(32) | user ID |
| `principal` | decimal(15, 2) | principal repayable |
| `instalment_fee` | decimal(15, 2) | interest repayable |
| `currency` | char(3) | currency |
| `loan_order_no` | varchar(64) | loan_order_no |
| `loan_order_id` | int | Loan order id |
| `create_time` | timestamp | create time |
| `update_time` | timestamp | update time |

## 主键 / 索引
- 主键:`id`
- `idx_order_no`:loan_order_no
- `idx_user_id`:user_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
