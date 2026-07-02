---
id: tbl_collection_sys_roles_depts
object_type: Table
name: 角色部门关联 (sys_roles_depts)
aliases: [sys_roles_depts, collection.sys_roles_depts]
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

# 角色部门关联 (sys_roles_depts)

## 用途
物理表 `collection.sys_roles_depts`,主键 `role_id, dept_id`。角色部门关联。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `role_id` | bigint | 角色 |
| `dept_id` | bigint | 部门 |

## 主键 / 索引
- 主键:`role_id, dept_id`
- `idx_dept`:dept_id

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
