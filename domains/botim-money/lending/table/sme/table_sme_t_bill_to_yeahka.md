---
id: tbl_sme_t_bill_to_yeahka
object_type: Table
name: Bill sheet (t_bill_to_yeahka)
aliases: [t_bill_to_yeahka, sme.t_bill_to_yeahka]
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

# Bill sheet (t_bill_to_yeahka)

## 用途
物理表 `sme.t_bill_to_yeahka`,主键 `id`。Bill sheet。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | 待补 · 可空 |
| `status` | smallint | Status: 0: to be effective, 1: to be repaid 2: settled |
| `period_num` | int | Which issue |
| `accrue_interest_time` | timestamp | Interest accrual time · 可空 |
| `due_time` | timestamp | Bill due date · 可空 |
| `settle_time` | timestamp | Settlement time · 可空 |
| `settle_way` | smallint | 待补 · 可空 |
| `cope_capital` | decimal(15, 2) | Principal repayable |
| `cope_interest` | decimal(15, 2) | Interest payable |
| `cope_penalty` | decimal(15, 2) | The penalty should be repaid · 可空 |
| `already_repay_capital` | decimal(15, 2) | Repaid principal |
| `already_repay_interest` | decimal(15, 2) | Interest paid |
| `already_repay_penalty` | decimal(15, 2) | The penalty interest has been repaid |
| `unaccrued_interest_waiver` | decimal(15, 2) | Waive unpaid interest |
| `currency` | char(3) | currency |
| `loan_order_no` | varchar(64) | order_no in table t_loan_order |
| `third_user_id` | varchar(20) | Third-party channel user id |
| `third_party_name` | varchar(20) | Order source channel name |
| `create_time` | timestamp | Creation time |
| `update_time` | timestamp | Modification time |

## 主键 / 索引
- 主键:`id`
- `idx_due_time`:due_time
- `idx_order_no`:loan_order_no
- `idx_user_id`:third_user_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
