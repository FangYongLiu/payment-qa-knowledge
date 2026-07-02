---
id: tbl_ccdeposit_t_binance_stock_inbound_order
object_type: Table
name: 币安资产入库 (t_binance_stock_inbound_order)
aliases: [t_binance_stock_inbound_order, ccdeposit.t_binance_stock_inbound_order]
domain: crypto
status: active
owner: can.wang
reviewer: can.wang
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: ccdeposit schema DDL
tags: [crypto, ccdeposit]
sensitivity: normal
related_services: []
---

# 币安资产入库 (t_binance_stock_inbound_order)

## 用途
物理表 `ccdeposit.t_binance_stock_inbound_order`,主键 `id`。币安资产入库。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | id |
| `txid` | varchar(200) | txid |
| `address` | varchar(64) | 待补 · 可空 |
| `chain_code` | varchar(32) | 待补 · 可空 |
| `insert_time` | timestamp(3) | insert_time · 可空 |

## 主键 / 索引
- 主键:`id`
- `uk_bsio_txid`:txid (UNIQUE)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
