---
id: tbl_aml_t_collection_mapping
object_type: Table
domain: compliance
status: active
owner: dewen.li
reviewer: dewen.li
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: aml schema DDL
tags:
- aml
- t_collection_mapping
subdomain: aml
module: null
sensitivity: normal
name: 分片映射表 (t_collection_mapping)
aliases:
- t_collection_mapping
- aml.t_collection_mapping
related_services: []
---

# 分片映射表 (t_collection_mapping)

## 用途
物理表 `aml.t_collection_mapping`,主键 `id`。sharding mapping collection。属 AML/合规库 `aml`。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补(compliance 域 AML 服务)。
- **谁读写它**:AML/风控链路的服务 / 接口(由对方文档 `related_tables` 声明)。
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
- **时间字段**:`create_time`/`update_time`;按时间过滤走对应索引。
- **关联交易**:`payment_order_no` 关联支付订单(风控/合规按订单聚合)。
- 更细的状态枚举、跨表关联与业务规则**待补**(需结合代码或业务文档)。
