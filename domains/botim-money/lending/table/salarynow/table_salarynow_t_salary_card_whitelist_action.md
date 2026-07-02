---
id: tbl_salarynow_t_salary_card_whitelist_action
object_type: Table
name: Salary card whitelist actions for scheduled processing (t_salary_card_whitelist_action)
aliases: [t_salary_card_whitelist_action, salarynow.t_salary_card_whitelist_action]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: salarynow schema DDL
tags: [lending, salarynow]
sensitivity: normal
related_services: []
---

# Salary card whitelist actions for scheduled processing (t_salary_card_whitelist_action)

## 用途
物理表 `salarynow.t_salary_card_whitelist_action`,主键 `id`。Salary card whitelist actions for scheduled processing。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | Primary key · 可空 |
| `member_id` | varchar(20) | Member identifier |
| `action_type` | varchar(32) | Action type: ADD, REMOVE |
| `action_status` | varchar(32) | Action status: PENDING, SUCCESS, FAILED |
| `error_message` | varchar(64) | Error message if action failed · 可空 |
| `action_time` | timestamp | Timestamp when action was processed · 可空 |
| `retry_count` | int | Number of retry attempts |
| `max_retries` | int | Maximum retry attempts |
| `create_time` | timestamp | Record creation timestamp |
| `update_time` | timestamp | Last update timestamp |

## 主键 / 索引
- 主键:`id`
- `idx_whitelist_action_member_id`:member_id
- `idx_whitelist_action_pending`:action_status, retry_count, max_retries

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
