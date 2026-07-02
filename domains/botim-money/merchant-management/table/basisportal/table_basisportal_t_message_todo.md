---
id: tbl_basisportal_t_message_todo
object_type: Table
name: Table for message todo (t_message_todo)
aliases: [t_message_todo, basisportal.t_message_todo]
domain: merchant-management
status: active
owner: yijian.tan
reviewer: yijian.tan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: basisportal schema DDL
tags: [merchant-management, basisportal]
sensitivity: normal
related_services: []
---

# Table for message todo (t_message_todo)

## 用途
物理表 `basisportal.t_message_todo`,主键 `id`。Table for message todo。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint(21) | 待补 |
| `source_system` | varchar(32) | The system message from · 可空 |
| `type` | varchar(64) | message type in source system · 可空 |
| `title` | varchar(128) | message title |
| `content` | varchar(255) | message content · 可空 |
| `url` | varchar(255) | The url of the page where can do audit · 可空 |
| `object_id` | varchar(32) | A unique identifier that identifies the application · 可空 |
| `receiver` | varchar(64) | The receiver's account · 可空 |
| `sender` | varchar(64) | account of sender · 可空 |
| `reviewer` | varchar(64) | account of reviewer · 可空 |
| `read_flag` | tinyint(1) | 0-unread 1-read |
| `deleted` | tinyint(1) | is deleted or not: 0-no 1-yes |
| `create_time` | timestamp | message create time · 可空 |
| `update_time` | timestamp | message update time · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_t_message_todo_object_id`:object_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
