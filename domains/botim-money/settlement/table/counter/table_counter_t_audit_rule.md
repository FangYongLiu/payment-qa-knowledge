---
id: tbl_counter_t_audit_rule
object_type: Table
name: Audit Application Rule (t_audit_rule)
aliases: [t_audit_rule, counter.t_audit_rule]
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

# Audit Application Rule (t_audit_rule)

## 用途
物理表 `counter.t_audit_rule`,主键 `rule_id`。Audit Application Rule。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `rule_id` | bigint | Rule ID |
| `audit_type` | varchar(16) | Audit Type |
| `rule_name` | varchar(100) | Rule Name · 可空 |
| `priority` | int(8) | Priority · 可空 |
| `matched_target` | varchar(500) | Matched Target · 可空 |
| `rule_content` | varchar(255) | Rule Content · 可空 |
| `status` | tinyint | Status · 可空 |
| `create_by` | bigint | Create User · 可空 |
| `create_time` | timestamp | Create Time · 可空 |
| `update_by` | bigint | Update User · 可空 |
| `update_time` | timestamp | Update Time · 可空 |

## 主键 / 索引
- 主键:`rule_id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
