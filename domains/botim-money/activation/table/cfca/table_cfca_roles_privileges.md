---
id: tbl_cfca_roles_privileges
object_type: Table
name: roles_privileges (roles_privileges)
aliases: [roles_privileges, cfca.roles_privileges]
domain: activation
status: active
owner: xinwei.cao
reviewer: xinwei.cao
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: cfca schema DDL
tags: [activation, cfca]
sensitivity: normal
related_services: []
---

# roles_privileges (roles_privileges)

## 用途
物理表 `cfca.roles_privileges`,主键 `role_id, priv_id`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `role_id` | bigint(11) | 待补 |
| `priv_id` | bigint(11) | 待补 |
| `foreign` | key | 待补 · 可空 |
| `foreign` | key | 待补 · 可空 |

## 主键 / 索引
- 主键:`role_id, priv_id`
- `IDX_ROLES_PRIVILEGES_PRIV_ID`:priv_id
- `IDX_ROLES_PRIVILEGES_ROLE_ID`:role_id

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
