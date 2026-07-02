---
id: tbl_collection_t_cs_feedback_action_record
object_type: Table
name: feedback action record (t_cs_feedback_action_record)
aliases: [t_cs_feedback_action_record, collection.t_cs_feedback_action_record]
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

# feedback action record (t_cs_feedback_action_record)

## 用途
物理表 `collection.t_cs_feedback_action_record`,主键 `id`。feedback action record。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | parme key · 可空 |
| `create_by` | varchar(50) | uid · 可空 |
| `create_time` | timestamp | time · 可空 |
| `update_by` | varchar(50) | uid · 可空 |
| `update_time` | timestamp | time · 可空 |
| `feedback_id` | bigint | feedback key |
| `member_id` | varchar(20) | customer memberId |
| `user_uid` | varchar(50) | user uid |
| `method` | tinyint(5) | 1:email us 2:call |
| `template` | varchar(50) | templateId · 可空 |
| `content` | varchar(1000) | content · 可空 |
| `action` | tinyint(5) | 0:open 1:close |
| `escalate` | tinyint(5) | 0:open 1:close |
| `call_id` | varchar(64) | call No · 可空 |
| `called_id_no` | bigint | call No index · 可空 |
| `email_id` | varchar(64) | eamil No · 可空 |
| `emailed_id_no` | bigint | eamil No index · 可空 |
| `call_status` | varchar(32) | call status · 可空 |
| `attachment` | varchar(200) | UFS tags for attachments, separated by newline characters · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_create_time`:create_time
- `idx_feedback_id`:feedback_id
- `idx_member_id`:member_id
- `idx_user_uid`:user_uid

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
