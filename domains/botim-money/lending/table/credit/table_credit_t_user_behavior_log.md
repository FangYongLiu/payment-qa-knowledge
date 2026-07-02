---
id: tbl_credit_t_user_behavior_log
object_type: Table
name: User behavior log table (t_user_behavior_log)
aliases: [t_user_behavior_log, credit.t_user_behavior_log]
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

# User behavior log table (t_user_behavior_log)

## 用途
物理表 `credit.t_user_behavior_log`,主键 `id`。User behavior log table。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | Primary key ID · 可空 |
| `user_id` | varchar(64) | User ID |
| `event_type` | varchar(32) | Event type: login, etc. |
| `risk_device_token` | varchar(128) | Token for tracking · 可空 |
| `device_id` | varchar(50) | Device ID · 可空 |
| `apdid` | varchar(64) | apdid (Ali device unique identifier) · 可空 |
| `created_time` | datetime | Created time · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_apdid`:apdid
- `idx_created_time`:created_time
- `idx_device_id`:device_id
- `idx_user_id`:user_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
