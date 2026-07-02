---
id: tbl_eminstalment_t_profile_change_log
object_type: Table
name: 用户信息修改记录表 (t_profile_change_log)
aliases: [t_profile_change_log, eminstalment.t_profile_change_log]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: eminstalment schema DDL
tags: [lending, eminstalment]
sensitivity: normal
related_services: []
---

# 用户信息修改记录表 (t_profile_change_log)

## 用途
物理表 `eminstalment.t_profile_change_log`,主键 `id`。用户信息修改记录表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int unsigned | 待补 · 可空 |
| `create_time` | timestamp | 创建日期 · 可空 |
| `last_modified` | timestamp | 修改日期 · 可空 |
| `user_id` | varchar(20) | 用户ID |
| `key_value` | varchar(32) | 字段名 |
| `before_value` | varchar(500) | 变更之前值 |
| `after_value` | varchar(500) | 变更之后值 |

## 主键 / 索引
- 主键:`id`
- `idx_user_id`:user_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
