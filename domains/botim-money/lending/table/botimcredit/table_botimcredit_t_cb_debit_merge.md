---
id: tbl_botimcredit_t_cb_debit_merge
object_type: Table
name: Merged auto debit records for user-level batch processing (t_cb_debit_merge)
aliases: [t_cb_debit_merge, botimcredit.t_cb_debit_merge]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: botimcredit schema DDL
tags: [lending, botimcredit]
sensitivity: normal
related_services: []
---

# Merged auto debit records for user-level batch processing (t_cb_debit_merge)

## 用途
物理表 `botimcredit.t_cb_debit_merge`,主键 `id`。Merged auto debit records for user-level batch processing。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | Primary key · 可空 |
| `user_id` | varchar(64) | User ID |
| `request_no` | varchar(32) | Unique request number for this batch |
| `amount` | decimal(19, 2) | Total debit amount |
| `principal` | decimal(19, 2) | Total principal amount · 可空 |
| `fee` | decimal(19, 2) | Total fee amount · 可空 |
| `penalty` | decimal(19, 2) | Total penalty amount · 可空 |
| `late_fee` | decimal(19, 2) | Total late fee amount · 可空 |
| `status` | tinyint | Status: 0-processing, 1-success, -1-failed |
| `config_id` | bigint | Config ID used for this debit (deprecated) · 可空 |
| `config_ids` | varchar(255) | Config IDs used for this debit (comma separated) · 可空 |
| `bill_nos` | varchar(255) | Bill numbers included in this batch (comma separated) · 可空 |
| `transaction_id` | varchar(128) | External transaction ID from payment gateway · 可空 |
| `response_msg` | varchar(50) | Response message from payment gateway · 可空 |
| `ext` | varchar(512) | Extension field for additional data (JSON) · 可空 |
| `created_time` | datetime | Created time |
| `updated_time` | datetime | Updated time |

## 主键 / 索引
- 主键:`id`
- `idx_config_id`:config_id
- `idx_request_no`:request_no
- `idx_user_id`:user_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
