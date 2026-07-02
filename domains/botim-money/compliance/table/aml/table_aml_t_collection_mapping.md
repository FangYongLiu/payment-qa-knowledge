---
id: tbl_aml_t_collection_mapping
object_type: Table
name: sharding mapping collection (t_collection_mapping)
aliases: [t_collection_mapping, aml.t_collection_mapping]
domain: compliance
status: active
owner: dewen.li
reviewer: dewen.li
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: aml schema DDL
tags: [compliance, aml]
sensitivity: normal
related_services: []
---

# sharding mapping collection (t_collection_mapping)

## 用途
物理表 `aml.t_collection_mapping`,主键 `id`。sharding mapping collection。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | id · 可空 |
| `payment_order_no` | varchar(64) | payment_order_no · 可空 |
| `transaction_id` | varchar(64) | transaction_id · 可空 |
| `tid` | varchar(64) | TID · 可空 |
| `collection_name` | varchar(32) | collection name |
| `create_time` | datetime | create_time |
| `update_time` | datetime | update_time |

## 主键 / 索引
- 主键:`id`
- `uk_payment_order_no`:payment_order_no (UNIQUE)
- `idx_tid`:tid
- `idx_transaction_id`:transaction_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
