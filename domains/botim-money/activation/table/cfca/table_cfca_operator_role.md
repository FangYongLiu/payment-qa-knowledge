---
id: tbl_cfca_operator_role
object_type: Table
name: operator_role (operator_role)
aliases: [operator_role, cfca.operator_role]
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

# operator_role (operator_role)

## 用途
物理表 `cfca.operator_role`,主键 `oper_id, role_id`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `oper_id` | bigint(11) | 待补 |
| `role_id` | bigint(11) | 待补 |
| `foreign` | key | 待补 · 可空 |
| `foreign` | key | 待补 · 可空 |

## 主键 / 索引
- 主键:`oper_id, role_id`
- `IDX_OPERATOR_ROLE_OPER_ID`:oper_id
- `IDX_OPERATOR_ROLE_ROLE_ID`:role_id

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
