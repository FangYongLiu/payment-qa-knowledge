---
id: tbl_rnpl_t_profile_change_log
object_type: Table
name: User Information Modification Record Table (t_profile_change_log)
aliases: [t_profile_change_log, rnpl.t_profile_change_log]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: rnpl schema DDL
tags: [lending, rnpl]
sensitivity: normal
related_services: []
---

# User Information Modification Record Table (t_profile_change_log)

## 用途
物理表 `rnpl.t_profile_change_log`,主键 `id`。User Information Modification Record Table。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int unsigned | 待补 · 可空 |
| `create_time` | timestamp | create time · 可空 |
| `last_modified` | timestamp | update time · 可空 |
| `user_id` | varchar(20) | user ID |
| `key_value` | varchar(32) | field name |
| `before_value` | varchar(500) | value before change |
| `after_value` | varchar(500) | value after change |

## 主键 / 索引
- 主键:`id`
- `idx_user_id`:user_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
