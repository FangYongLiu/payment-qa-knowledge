---
id: tbl_cctrade_t_trade_order_participation
object_type: Table
name: 交易参与 (t_trade_order_participation)
aliases: [t_trade_order_participation, cctrade.t_trade_order_participation]
domain: crypto
status: active
owner: can.wang
reviewer: can.wang
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: cctrade schema DDL
tags: [crypto, cctrade]
sensitivity: normal
related_services: []
---

# 交易参与 (t_trade_order_participation)

## 用途
物理表 `cctrade.t_trade_order_participation`,主键 `id`。交易参与。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | id |
| `trade_order_id` | bigint | 交易订单号 |
| `participator_code` | varchar(32) | 参与方代码 |
| `participator_type` | varchar(16) | 参与方类型 |
| `role` | varchar(32) | 角色 |
| `currency_code` | varchar(32) | 币种 · 可空 |
| `amount` | decimal(23, 8) | 金额 · 可空 |

## 主键 / 索引
- 主键:`id`
- `i_top_td`:trade_order_id

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
