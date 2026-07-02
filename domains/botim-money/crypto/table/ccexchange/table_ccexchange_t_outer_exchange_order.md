---
id: tbl_ccexchange_t_outer_exchange_order
object_type: Table
name: 外部兑换订单 (t_outer_exchange_order)
aliases: [t_outer_exchange_order, ccexchange.t_outer_exchange_order]
domain: crypto
status: active
owner: can.wang
reviewer: can.wang
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: ccexchange schema DDL
tags: [crypto, ccexchange]
sensitivity: normal
related_services: []
---

# 外部兑换订单 (t_outer_exchange_order)

## 用途
物理表 `ccexchange.t_outer_exchange_order`,主键 `id`。外部兑换订单。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | id |
| `gain_or_loss_crcy` | varchar(32) | 盈亏币种 · 可空 |
| `gain_or_loss_amt` | decimal(23, 8) | 盈亏金额 · 可空 |
| `expired_time` | timestamp(3) | 超时时间 · 可空 |
| `supplier_order_id` | varchar(50) | 供应商订单号 · 可空 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
