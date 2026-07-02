---
id: tbl_officer_sys_roles_depts
object_type: Table
name: Role department association (sys_roles_depts)
aliases: [sys_roles_depts, officer.sys_roles_depts]
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

# Role department association (sys_roles_depts)

## 用途
物理表 `officer.sys_roles_depts`,主键 `role_id, dept_id`。Role department association。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `role_id` | bigint | Role |
| `dept_id` | bigint | Department |

## 主键 / 索引
- 主键:`role_id, dept_id`
- `idx_dept`:dept_id

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
