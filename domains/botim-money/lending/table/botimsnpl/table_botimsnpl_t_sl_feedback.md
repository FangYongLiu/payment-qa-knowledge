---
id: tbl_botimsnpl_t_sl_feedback
object_type: Table
name: feedback (t_sl_feedback)
aliases: [t_sl_feedback, botimsnpl.t_sl_feedback]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: botimsnpl schema DDL
tags: [lending, botimsnpl]
sensitivity: normal
related_services: []
---

# feedback (t_sl_feedback)

## 用途
物理表 `botimsnpl.t_sl_feedback`,主键 `id`。feedback。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | 主键 · 可空 |
| `context` | varchar(1000) | context · 可空 |
| `user_id` | varchar(20) | user id · 可空 |
| `easy_to_use` | smallint | easy to use |
| `fees` | smallint | fees |
| `message` | varchar(1000) | message · 可空 |
| `experience` | smallint | experience |
| `credit_amount` | smallint | credit_amount |
| `ext` | varchar(255) | ext · 可空 |
| `create_time` | timestamp | 待补 |
| `update_time` | timestamp | 待补 |

## 主键 / 索引
- 主键:`id`
- `idx_user_id`:user_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
