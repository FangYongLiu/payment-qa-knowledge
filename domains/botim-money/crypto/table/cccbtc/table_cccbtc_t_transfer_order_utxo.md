---
id: tbl_cccbtc_t_transfer_order_utxo
object_type: Table
name: t_transfer_order_utxo (t_transfer_order_utxo)
aliases: [t_transfer_order_utxo, cccbtc.t_transfer_order_utxo]
domain: crypto
status: active
owner: can.wang
reviewer: can.wang
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: cccbtc schema DDL
tags: [crypto, cccbtc]
sensitivity: normal
related_services: []
---

# t_transfer_order_utxo (t_transfer_order_utxo)

## 用途
物理表 `cccbtc.t_transfer_order_utxo`,主键 `ID, utxo_id`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `ID` | bigint | 待补 |
| `utxo_id` | bigint | id(yyyyMMdd999999999) |

## 主键 / 索引
- 主键:`ID, utxo_id`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
