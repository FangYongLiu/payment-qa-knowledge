---
id: tbl_ccceth_t_eth_deposit_event
object_type: Table
name: eth充值事件(分区) (t_eth_deposit_event)
aliases: [t_eth_deposit_event, ccceth.t_eth_deposit_event]
domain: crypto
status: active
owner: can.wang
reviewer: can.wang
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: ccceth schema DDL
tags: [crypto, ccceth]
sensitivity: normal
related_services: []
---

# eth充值事件(分区) (t_eth_deposit_event)

## 用途
物理表 `ccceth.t_eth_deposit_event`,主键 `id`。eth充值事件(分区)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | id(yyyyMMdd999999999) |
| `unique_tx_hash` | varchar(200) | 唯一事务hash |

## 主键 / 索引
- 主键:`id`
- `uk_eth_de_tx`:unique_tx_hash (UNIQUE)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
