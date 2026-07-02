---
id: tbl_rnpl_t_contract_check_item
object_type: Table
name: Contract Check Item Table (t_contract_check_item)
aliases: [t_contract_check_item, rnpl.t_contract_check_item]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: rnpl schema DDL
tags: [lending, rnpl]
sensitivity: normal
related_services: []
---

# Contract Check Item Table (t_contract_check_item)

## 用途
物理表 `rnpl.t_contract_check_item`,主键 `id`。Contract Check Item Table。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | 待补 · 可空 |
| `contract_id` | int | contract ID |
| `item_name` | varchar(32) | check item name |
| `status` | smallint | check item status: 0: pending confirmation; 1: confirmed |
| `receive_date` | timestamp | time of receipt of documents offline for Check items · 可空 |
| `create_time` | timestamp | 待补 |
| `update_time` | timestamp | 待补 |

## 主键 / 索引
- 主键:`id`
- `idx_contractId`:contract_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
