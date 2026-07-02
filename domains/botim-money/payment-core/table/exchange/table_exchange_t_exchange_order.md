---
id: tbl_exchange_t_exchange_order
object_type: Table
name: t_exchange_order (t_exchange_order)
aliases: [t_exchange_order, exchange.t_exchange_order]
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: exchange schema DDL
tags: [payment-core, exchange]
sensitivity: normal
related_services: []
---

# t_exchange_order (t_exchange_order)

## 用途
物理表 `exchange.t_exchange_order`,主键 `product_order_no`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `product_order_no` | bigint(18) | 产品订单号 |
| `trade_order_no` | varchar(32) | 交易订单号 · 可空 |
| `source_amount` | decimal(19, 4) | Source Amount · 可空 |
| `source_currency` | varchar(3) | 源币种 · 可空 |
| `target_amount` | decimal(19, 4) | Target Amount · 可空 |
| `target_currency` | varchar(3) | 目标币种 · 可空 |
| `status` | varchar(1) | 状态 · 可空 |
| `cost` | decimal(19, 4) | Cost · 可空 |
| `payer_account_no` | varchar(32) | 付方账号 · 可空 |
| `payer_id` | varchar(16) | 付款方id · 可空 |
| `payee_account_no` | varchar(32) | 收款方账号 · 可空 |
| `payee_id` | varchar(16) | 收款方id · 可空 |
| `gmt_create` | timestamp | 创建时间 · 可空 |
| `gmt_modified` | timestamp | 修改时间 · 可空 |

## 主键 / 索引
- 主键:`product_order_no`
- 无(仅主键)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
