---
id: tbl_botimsnpl_t_sl_contact_temp
object_type: Table
name: temp table for sync (t_sl_contact_temp)
aliases: [t_sl_contact_temp, botimsnpl.t_sl_contact_temp]
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

# temp table for sync (t_sl_contact_temp)

## 用途
物理表 `botimsnpl.t_sl_contact_temp`,主键 `id`。temp table for sync。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int unsigned | ID · 可空 |
| `user_id` | varchar(20) | user ID |
| `create_time` | datetime | create time |
| `update_time` | datetime | update time |

## 主键 / 索引
- 主键:`id`
- `idx_user_id`:user_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
