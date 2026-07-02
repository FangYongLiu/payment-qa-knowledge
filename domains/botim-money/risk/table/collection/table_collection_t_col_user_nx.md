---
id: tbl_collection_t_col_user_nx
object_type: Table
name: 牛信账户关联表 (t_col_user_nx)
aliases: [t_col_user_nx, collection.t_col_user_nx]
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

# 牛信账户关联表 (t_col_user_nx)

## 用途
物理表 `collection.t_col_user_nx`,主键 `id`。牛信账户关联表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint(11) | 主键 · 可空 |
| `create_by` | varchar(100) | 创建者 · 可空 |
| `create_time` | timestamp | 创建时间 · 可空 |
| `update_time` | timestamp | 更新时间 · 可空 |
| `update_by` | varchar(100) | 更新人员 · 可空 |
| `nx_no` | varchar(50) | 牛信账户 |
| `user_uid` | varchar(100) | 用户uid |
| `enabled` | tinyint | 是否启用 |

## 主键 / 索引
- 主键:`id`
- `inx_phone`:user_uid

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
