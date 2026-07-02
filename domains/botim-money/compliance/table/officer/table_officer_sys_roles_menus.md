---
id: tbl_officer_sys_roles_menus
object_type: Table
name: Role menu association (sys_roles_menus)
aliases: [sys_roles_menus, officer.sys_roles_menus]
domain: compliance
status: active
owner: dewen.li
reviewer: dewen.li
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: officer schema DDL
tags: [compliance, officer]
sensitivity: normal
related_services: []
---

# Role menu association (sys_roles_menus)

## 用途
物理表 `officer.sys_roles_menus`,主键 `menu_id, role_id`。Role menu association。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `menu_id` | bigint | Menu ID |
| `role_id` | bigint | Role ID |

## 主键 / 索引
- 主键:`menu_id, role_id`
- `idx_role`:role_id

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
