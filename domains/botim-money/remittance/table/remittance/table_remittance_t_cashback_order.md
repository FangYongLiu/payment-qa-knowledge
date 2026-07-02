---
id: tbl_remittance_t_cashback_order
object_type: Table
name: Cashback order master table (t_cashback_order)
aliases: [t_cashback_order, remittance.t_cashback_order]
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

# Cashback order master table (t_cashback_order)

## 用途
物理表 `remittance.t_cashback_order`,主键 `id`。Cashback order master table。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | Primary key · 可空 |
| `payee_id` | varchar(20) | payee id · 可空 |
| `order_no` | bigint | Source order number |
| `cashback_amount` | decimal(20, 2) | Cashback amount · 可空 |
| `currency` | char(3) | Currency code · 可空 |
| `partner_id` | varchar(50) | partner_id · 可空 |
| `biz_product_code` | varchar(10) | Biz product code · 可空 |
| `status` | varchar(20) | Status: INIT/PROCESSING/SUCCESS/FAILED |
| `remark` | varchar(255) | Remark · 可空 |
| `create_time` | timestamp | Create time |
| `update_time` | timestamp | Update time |

## 主键 / 索引
- 主键:`id`
- `uk_order_no`:order_no (UNIQUE)
- `idx_status_create_time`:status, update_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
