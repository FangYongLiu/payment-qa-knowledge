---
id: tbl_aml_t_user_verify
object_type: Table
name: User identity verification task (t_user_verify)
aliases: [t_user_verify, aml.t_user_verify]
domain: compliance
status: active
owner: dewen.li
reviewer: dewen.li
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: aml schema DDL
tags: [compliance, aml]
sensitivity: normal
related_services: []
---

# User identity verification task (t_user_verify)

## 用途
物理表 `aml.t_user_verify`,主键 `id`。User identity verification task。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | Primary key leaf id |
| `member_id` | varchar(32) | Member id |
| `event_type` | varchar(32) | Event type e.g. USER_VERIFY |
| `identity_type` | varchar(32) | Verification modes PASSWORD LIVE_DETECT comma-separated · 可空 |
| `task_status` | varchar(16) | INI created NTF notified SUC pass FAL fail EXP expired |
| `notify_status` | varchar(16) | PNS last SUCCESS FAILED · 可空 |
| `cis_ticket` | varchar(32) | Unique CIS ticket; written by GRC after chain (NULL until then) · 可空 |
| `verify_result` | varchar(16) | PASS FAIL · 可空 |
| `expire_time` | timestamp(3) | Task expiry |
| `remarks` | varchar(255) | Remarks · 可空 |
| `create_time` | timestamp | Created at · 可空 |
| `update_time` | timestamp | Updated at · 可空 |
| `create_by` | varchar(32) | Created by · 可空 |
| `update_by` | varchar(32) | Updated by · 可空 |

## 主键 / 索引
- 主键:`id`
- `uk_cis_ticket`:cis_ticket (UNIQUE)
- `idx_member_create_time`:member_id, create_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
