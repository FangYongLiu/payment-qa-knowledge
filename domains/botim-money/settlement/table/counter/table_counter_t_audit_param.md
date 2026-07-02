---
id: tbl_counter_t_audit_param
object_type: Table
name: 审核参数表 (t_audit_param)
aliases: [t_audit_param, counter.t_audit_param]
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

# 审核参数表 (t_audit_param)

## 用途
物理表 `counter.t_audit_param`,主键 `param_id`。审核参数表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `param_id` | bigint(17) | 主键 |
| `audit_id` | bigint(17) | 审核记录ID · 可空 |
| `param_key` | varchar(32) | 参数key · 可空 |
| `param_value` | varchar(20000) | 参数value · 可空 |

## 主键 / 索引
- 主键:`param_id`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
