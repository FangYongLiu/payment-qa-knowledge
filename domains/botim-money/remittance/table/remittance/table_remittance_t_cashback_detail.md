---
id: tbl_remittance_t_cashback_detail
object_type: Table
name: Cashback detail table (records each retry attempt) (t_cashback_detail)
aliases: [t_cashback_detail, remittance.t_cashback_detail]
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

# Cashback detail table (records each retry attempt) (t_cashback_detail)

## 用途
物理表 `remittance.t_cashback_detail`,主键 `id`。Cashback detail table (records each retry attempt)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | Primary key · 可空 |
| `cashback_id` | bigint | Foreign key to remittance.t_cashback_order.id |
| `order_no` | bigint | Source order number |
| `cashback_order_no` | bigint | Cashback order number (new for each retry) |
| `status` | varchar(20) | Status: PROCESSING/SUCCESS/FAILED/CANCELLED |
| `fail_reason` | varchar(500) | Failure reason · 可空 |
| `create_time` | timestamp | Create time |
| `update_time` | timestamp | Update time |

## 主键 / 索引
- 主键:`id`
- `idx_cashback_id`:cashback_id
- `idx_cashback_order_no`:cashback_order_no
- `idx_status_update_time`:status, update_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
