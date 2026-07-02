---
id: tbl_remittance_t_channel_status_log
object_type: Table
name: Channel status change log for monitoring success rate and balance (t_channel_status_log)
aliases: [t_channel_status_log, remittance.t_channel_status_log]
domain: remittance
status: active
owner: lei.pan
reviewer: lei.pan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: remittance schema DDL
tags: [remittance, remittance]
sensitivity: normal
related_services: []
---

# Channel status change log for monitoring success rate and balance (t_channel_status_log)

## 用途
物理表 `remittance.t_channel_status_log`,主键 `id`。Channel status change log for monitoring success rate and balance。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | Primary key · 可空 |
| `channel_code` | varchar(32) | Channel code |
| `status_type` | varchar(20) | Status type: SUCCESS_RATE, BALANCE |
| `event_type` | varchar(20) | Event type: FALL (enter blacklist), RECOVER (exit blacklist) |
| `threshold` | decimal(20, 6) | Threshold value (success rate threshold or minimum balance requirement) · 可空 |
| `current_value` | decimal(20, 6) | Current value (current success rate or current balance) · 可空 |
| `fall_time` | timestamp | Fall time (when entered blacklist) · 可空 |
| `recover_time` | timestamp | Recover time (when exited blacklist, only for RECOVER events) · 可空 |
| `duration_minutes` | bigint | Duration in minutes (only for RECOVER events) · 可空 |
| `remark` | varchar(255) | Remark · 可空 |
| `created_at` | timestamp | Created time |
| `updated_at` | timestamp | Updated time |

## 主键 / 索引
- 主键:`id`
- `idx_channel_created`:channel_code, created_at
- `idx_created_at`:created_at

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
