---
id: tbl_reconciliation_t_fund_allocate_detail
object_type: Table
name: Fund Allocate Detail (t_fund_allocate_detail)
aliases: [t_fund_allocate_detail, reconciliation.t_fund_allocate_detail]
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

# Fund Allocate Detail (t_fund_allocate_detail)

## 用途
物理表 `reconciliation.t_fund_allocate_detail`,主键 `detail_id`。Fund Allocate Detail。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `detail_id` | bigint | Detail Id: 8 digits date + 9 digits sequence |
| `sync_progress_id` | bigint | Sync Progress Id |
| `bank_code` | varchar(32) | Bank Code |
| `channel_ref_id` | varchar(50) | Channel Ref Id |
| `virtual_account` | varchar(50) | Virtual Account · 可空 |
| `part_type` | varchar(32) | Part Type · 可空 |
| `account_id` | varchar(32) | Account Id |
| `account_name` | varchar(255) | Account Name · 可空 |
| `value_date` | timestamp | Value Date · 可空 |
| `post_date` | timestamp | Post Date · 可空 |
| `transaction_type` | varchar(10) | Transaction Type: Credit Debit |
| `instructed_amount` | decimal(19, 4) | Instructed Amount |
| `instructed_currency` | char(3) | Instructed Currency |
| `transaction_amount` | decimal(19, 4) | Transaction Amount |
| `transaction_currency` | char(3) | Transaction Currency |
| `balance` | decimal(19, 4) | Balance: todo:currency |
| `instruction_identification` | varchar(128) | Instruction Identification · 可空 |
| `beneficiary_account` | varchar(32) | Beneficiary Account · 可空 |
| `beneficiary_details` | varchar(255) | Beneficiary Details |
| `description` | varchar(255) | description · 可空 |
| `remarks` | varchar(255) | Remarks · 可空 |
| `action_batch_id` | bigint | Action Batch Id · 可空 |
| `extension` | varchar(255) | Extension · 可空 |
| `create_time` | timestamp | Create time |
| `update_time` | timestamp | Update time |

## 主键 / 索引
- 主键:`detail_id`
- `idx_batchid`:action_batch_id
- `idx_post_date`:post_date
- `idx_refid`:channel_ref_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
