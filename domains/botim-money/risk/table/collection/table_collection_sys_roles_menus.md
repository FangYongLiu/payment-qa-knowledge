---
id: tbl_collection_sys_roles_menus
object_type: Table
name: 角色菜单关联 (sys_roles_menus)
aliases: [sys_roles_menus, collection.sys_roles_menus]
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

# 角色菜单关联 (sys_roles_menus)

## 用途
物理表 `collection.sys_roles_menus`,主键 `menu_id, role_id`。角色菜单关联。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `menu_id` | bigint | 菜单ID |
| `role_id` | bigint | 角色ID |

## 主键 / 索引
- 主键:`menu_id, role_id`
- `idx_role`:role_id

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
