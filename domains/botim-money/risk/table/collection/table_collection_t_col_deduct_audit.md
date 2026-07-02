---
id: tbl_collection_t_col_deduct_audit
object_type: Table
name: Approval Request Table (t_col_deduct_audit)
aliases: [t_col_deduct_audit, collection.t_col_deduct_audit]
domain: risk
status: active
owner: xinwei.cao,dewen.li
reviewer: xinwei.cao,dewen.li
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: collection schema DDL
tags: [risk, collection]
sensitivity: normal
related_services: []
---

# Approval Request Table (t_col_deduct_audit)

## 用途
物理表 `collection.t_col_deduct_audit`,主键 `id`。Approval Request Table。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | Primary Key ID · 可空 |
| `member_id` | varchar(20) | Member ID |
| `phone_number` | varchar(32) | Phone Number · 可空 |
| `product` | varchar(20) | Product Name · 可空 |
| `bill_no` | varchar(64) | Bill number from t_col_bill · 可空 |
| `stage` | varchar(32) | Stage · 可空 |
| `deduct_type` | tinyint | Deduction Type (1:Late Fee Coupon, 2:Interest Late Fee Coupon, 3:Deduction) |
| `deduct_amount` | decimal(15, 2) | Deduction Amount · 可空 |
| `uuid` | varchar(64) | Unique reference ID from t_cs_repay_record |
| `paid_loan_amount` | decimal(15, 2) | Paid Loan Amount · 可空 |
| `total_paid_interest_fee` | decimal(15, 2) | Total Paid Interest and Late Fee · 可空 |
| `status` | tinyint | Approval Status (0:Submitted, 1:Approved, -1:Rejected, -2:Approved but action failed, 2:Approved and action succeeded) |
| `created_by` | varchar(100) | Submitter |
| `reason` | varchar(200) | Application Reason · 可空 |
| `file_tag_list` | varchar(128) | File Tag · 可空 |
| `action_by` | varchar(100) | Approver · 可空 |
| `comments` | varchar(200) | Approval Comments · 可空 |
| `approved_time` | timestamp | Approval Time · 可空 |
| `create_time` | timestamp | Creation timestamp |
| `update_time` | timestamp | Last update timestamp |

## 主键 / 索引
- 主键:`id`
- `uk_uuid`:uuid (UNIQUE)
- `idx_bill_no`:bill_no
- `idx_create_time`:create_time
- `idx_member_id`:member_id
- `idx_phone_number`:phone_number

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
