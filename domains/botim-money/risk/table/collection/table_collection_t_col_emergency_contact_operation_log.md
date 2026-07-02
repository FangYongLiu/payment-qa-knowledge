---
id: tbl_collection_t_col_emergency_contact_operation_log
object_type: Table
name: Emergency Contact Operation Log Table (t_col_emergency_contact_operation_log)
aliases: [t_col_emergency_contact_operation_log, collection.t_col_emergency_contact_operation_log]
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

# Emergency Contact Operation Log Table (t_col_emergency_contact_operation_log)

## 用途
物理表 `collection.t_col_emergency_contact_operation_log`,主键 `id`。Emergency Contact Operation Log Table。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | Primary Key ID · 可空 |
| `user_uid` | varchar(50) | Operation User UID |
| `user_name` | varchar(128) | Operation User Name |
| `member_id` | varchar(20) | Member ID · 可空 |
| `removed_contact_name` | varchar(128) | Name of Removed Emergency Contact · 可空 |
| `removed_contact_phone` | varchar(32) | Phone of Removed Emergency Contact · 可空 |
| `create_time` | timestamp | Creation Time · 可空 |
| `update_time` | timestamp | Update Time · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_create_time`:create_time
- `idx_member_id`:member_id
- `idx_user_uid`:user_uid

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
