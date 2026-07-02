---
id: tbl_ccexchange_t_trade_history
object_type: Table
name: 交易历史 (t_trade_history)
aliases: [t_trade_history, ccexchange.t_trade_history]
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

# 交易历史 (t_trade_history)

## 用途
物理表 `ccexchange.t_trade_history`,主键 `id`。交易历史。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | id |
| `trade_id` | varchar(50) | 交易id |
| `order_id` | varchar(50) | 订单id |
| `commission_crcy` | varchar(32) | 佣金币种 |
| `commission` | decimal(23, 8) | 佣金金额 |
| `base_currency_code` | varchar(32) | 本位币币种 |
| `base_amount` | decimal(23, 8) | 本位币金额 |
| `symbol` | varchar(32) | symbol |
| `created_time` | timestamp(3) | 创建时间 |
| `quote_amount` | decimal(23, 8) | 报价金额 · 可空 |
| `quote_currency_code` | varchar(32) | 报价币种 · 可空 |
| `trade_time` | timestamp(3) | 交易时间 · 可空 |

## 主键 / 索引
- 主键:`id`
- `uk_th_trade_symbol`:trade_id, symbol, order_id (UNIQUE)
- `i_th_ct`:created_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
