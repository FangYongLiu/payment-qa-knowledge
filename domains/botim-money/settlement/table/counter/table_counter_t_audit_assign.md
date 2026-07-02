---
id: tbl_counter_t_audit_assign
object_type: Table
name: Audit Assign (t_audit_assign)
aliases: [t_audit_assign, counter.t_audit_assign]
domain: settlement
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: counter schema DDL
tags: [settlement, counter]
sensitivity: normal
related_services: []
---

# Audit Assign (t_audit_assign)

## 用途
物理表 `counter.t_audit_assign`,主键 `id`。Audit Assign。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | ID |
| `audit_id` | bigint | Audit record ID |
| `role_id` | bigint | Role ID |

## 主键 / 索引
- 主键:`id`
- `idx_audit_assign_role_id`:role_id

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
