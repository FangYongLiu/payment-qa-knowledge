---
id: tbl_collection_t_col_audio_record
object_type: Table
name: audio call task record (t_col_audio_record)
aliases: [t_col_audio_record, collection.t_col_audio_record]
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

# audio call task record (t_col_audio_record)

## 用途
物理表 `collection.t_col_audio_record`,主键 `id`。audio call task record。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | prime key · 可空 |
| `create_time` | timestamp | create_time · 可空 |
| `update_time` | timestamp | update_time · 可空 |
| `session_id` | varchar(45) | date-hour-pusconfigId-index |
| `member_id` | varchar(20) | debtor memberId |
| `order_no` | varchar(50) | order No |
| `status` | tinyint(5) | 0:init 1:sendSuccess 2:finish |
| `call_status` | tinyint(5) | 0:init 1:success -1:fail -2:userRefuse -3:unAnswer |
| `duration` | tinyint(5) | seconds |
| `start_time` | timestamp | start_time · 可空 |
| `answer_time` | timestamp | answer_time · 可空 |
| `end_time` | timestamp | end_time · 可空 |
| `phone` | varchar(30) | +971-5xxxxxxx · 可空 |
| `country_code` | varchar(10) | 971 · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_member_id`:member_id
- `idx_phone`:phone
- `idx_session_id`:session_id
- `idx_start_time`:start_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
