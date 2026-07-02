---
id: tbl_collection_t_cs_feedback
object_type: Table
name: feedback (t_cs_feedback)
aliases: [t_cs_feedback, collection.t_cs_feedback]
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

# feedback (t_cs_feedback)

## 用途
物理表 `collection.t_cs_feedback`,主键 `id`。feedback。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | prime key · 可空 |
| `create_by` | varchar(50) | uid · 可空 |
| `create_time` | timestamp | time · 可空 |
| `update_by` | varchar(50) | uid · 可空 |
| `update_time` | timestamp | time · 可空 |
| `member_id` | varchar(20) | customer memberId |
| `channel` | tinyint(5) | 1:help us 2:whatsapp 3:email |
| `name` | varchar(100) | 待补 · 可空 |
| `email` | varchar(50) | 待补 · 可空 |
| `category` | varchar(50) | type |
| `subcategory` | varchar(64) | sub type · 可空 |
| `best_contact_time` | varchar(50) | best time string · 可空 |
| `message` | varchar(1000) | message content |
| `attachment` | varchar(100) | file tag · 可空 |
| `phone` | varchar(30) | phone |
| `user_uid` | varchar(50) | user uid |
| `status` | tinyint(5) | 0:open 10:close |
| `bill_id` | bigint | t_cs_feedback_bill key · 可空 |
| `call_status` | varchar(32) | call status · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_bill_id`:bill_id
- `idx_create_time`:create_time
- `idx_member_id`:member_id
- `idx_phone`:phone
- `idx_user_uid`:user_uid

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
