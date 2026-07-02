---
id: tbl_credit_t_cs_bill_change_log
object_type: Table
name: Bill field change log (t_cs_bill_change_log)
aliases: [t_cs_bill_change_log, credit.t_cs_bill_change_log]
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

# Bill field change log (t_cs_bill_change_log)

## 用途
物理表 `credit.t_cs_bill_change_log`,主键 `id`。Bill field change log。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | Primary key · 可空 |
| `bill_id` | int | Bill ID from t_cs_bill.id |
| `order_no` | varchar(64) | Order number |
| `user_id` | varchar(20) | User ID |
| `change_field_name` | varchar(32) | Changed field name, e.g. due_time/cope_penalty |
| `change_action` | varchar(16) | Action type: APPLY/ROLLBACK |
| `old_value` | varchar(64) | Value before change (string) |
| `new_value` | varchar(64) | Value after change (string) |
| `original_value` | varchar(64) | Original value at first change · 可空 |
| `change_reason` | varchar(255) | Reason for change · 可空 |
| `change_params` | varchar(255) | Change parameters in JSON string · 可空 |
| `status` | varchar(16) | Status: PENDING/PROCESSING/SUCCESS/FAILED/ROLLED_BACK |
| `error_message` | varchar(255) | Failure reason · 可空 |
| `operator` | varchar(32) | Operator · 可空 |
| `operator_ip` | varchar(45) | Operator IP · 可空 |
| `operator_role` | varchar(16) | Operator role: ADMIN/SYSTEM/API · 可空 |
| `created_time` | timestamp | Creation time |
| `last_modified` | timestamp | Last update time |
| `executed_time` | timestamp | Execution time · 可空 |
| `rolled_back_time` | timestamp | Rollback time · 可空 |
| `parent_log_id` | bigint | Parent log ID for rollback link · 可空 |
| `batch_id` | varchar(64) | Batch ID · 可空 |
| `source` | varchar(32) | Source: ADMIN_API/BATCH_JOB/CUSTOMER_REQUEST |
| `bill_before_snapshot` | varchar(1024) | Bill snapshot before change (JSON string) · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_batch_id`:batch_id
- `idx_bill_id`:bill_id
- `idx_order_no`:order_no
- `idx_user_id`:user_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
