---
id: tbl_remittance_t_dyn_rule_condition
object_type: Table
name: Rule Condition Detail Table (Support Single Condition Object and Multi-Condition Array) (t_dyn_rule_condition)
aliases: [t_dyn_rule_condition, remittance.t_dyn_rule_condition]
domain: remittance
status: active
owner: lei.pan
reviewer: lei.pan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: remittance schema DDL
tags: [remittance, remittance]
sensitivity: normal
related_services: []
---

# Rule Condition Detail Table (Support Single Condition Object and Multi-Condition Array) (t_dyn_rule_condition)

## 用途
物理表 `remittance.t_dyn_rule_condition`,主键 `id`。Rule Condition Detail Table (Support Single Condition Object and Multi-Condition Array)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | Primary Key ID · 可空 |
| `rule_id` | bigint | Rule ID (Foreign Key: t_dyn_rule.id) |
| `condition_index` | int | Condition Index (position in array, 0 for single condition) |
| `fact` | varchar(64) | Condition Field Name (e.g.: receiveCountry, channelCode) |
| `operator` | varchar(16) | Operator (e.g.: IN, =, >, <, >=, <=, !=) |
| `value_item` | varchar(64) | Condition Value Item (single value, e.g.: CN, PH, WEIXIN) |
| `value_index` | int | Value Order Index (value order within same condition) |
| `gmt_create` | timestamp | Create Time |
| `gmt_modified` | timestamp | Modify Time |

## 主键 / 索引
- 主键:`id`
- `idx_rule_id`:rule_id

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
