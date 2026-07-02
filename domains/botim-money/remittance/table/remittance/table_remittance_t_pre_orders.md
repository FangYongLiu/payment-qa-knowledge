---
id: tbl_remittance_t_pre_orders
object_type: Table
name: pre orders table (t_pre_orders)
aliases: [t_pre_orders, remittance.t_pre_orders]
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

# pre orders table (t_pre_orders)

## 用途
物理表 `remittance.t_pre_orders`,主键 `id`。pre orders table。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | id · 可空 |
| `order_no` | bigint | order no |
| `pre_type` | varchar(20) | pre type |
| `status` | char | status : I- processing,S- success |
| `create_time` | timestamp | create time |
| `update_time` | timestamp | update time |

## 主键 / 索引
- 主键:`id`
- `idx_order_no`:order_no
- `idx_update_time`:update_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
