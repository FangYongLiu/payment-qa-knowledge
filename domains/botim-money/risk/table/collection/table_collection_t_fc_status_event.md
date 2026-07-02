---
id: tbl_collection_t_fc_status_event
object_type: Table
name: 用户状态事件表 (t_fc_status_event)
aliases: [t_fc_status_event, collection.t_fc_status_event]
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

# 用户状态事件表 (t_fc_status_event)

## 用途
物理表 `collection.t_fc_status_event`,主键 `id`。用户状态事件表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint(10) | 主键 · 可空 |
| `create_by` | varchar(50) | 创建者 · 可空 |
| `update_by` | varchar(50) | 更新人员 · 可空 |
| `create_time` | timestamp | 创建时间 · 可空 |
| `update_time` | timestamp | 更新时间 · 可空 |
| `user_uid` | varchar(50) | 用户id |
| `type` | tinyint(5) | -1 logout 1:available 2:busy 3:ptp 4:lunch 5:small · 可空 |
| `stage_name` | varchar(10) | 账龄 |

## 主键 / 索引
- 主键:`id`
- `idx_create_time`:create_time
- `idx_user_uid`:user_uid

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
