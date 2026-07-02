---
id: tbl_collection_sys_role
object_type: Table
name: 角色表 (sys_role)
aliases: [sys_role, collection.sys_role]
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

# 角色表 (sys_role)

## 用途
物理表 `collection.sys_role`,主键 `role_id`。角色表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `role_id` | bigint | ID · 可空 |
| `name` | varchar(255) | 名称 |
| `level` | int(255) | 角色级别 · 可空 |
| `description` | varchar(100) | 描述 · 可空 |
| `data_scope` | varchar(100) | 数据权限 · 可空 |
| `create_by` | varchar(100) | 创建者 · 可空 |
| `update_by` | varchar(100) | 更新者 · 可空 |
| `create_time` | timestamp | 创建日期 · 可空 |
| `update_time` | timestamp | 更新时间 · 可空 |

## 主键 / 索引
- 主键:`role_id`
- `uk_uniq_name`:name (UNIQUE)
- `idx_role`:name

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
