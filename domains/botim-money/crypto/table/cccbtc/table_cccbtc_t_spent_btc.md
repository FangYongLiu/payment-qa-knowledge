---
id: tbl_cccbtc_t_spent_btc
object_type: Table
name: t_spent_btc (t_spent_btc)
aliases: [t_spent_btc, cccbtc.t_spent_btc]
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

# t_spent_btc (t_spent_btc)

## 用途
物理表 `cccbtc.t_spent_btc`,主键 `ID`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `ID` | bigint | 待补 |
| `TX_HASH` | varchar(100) | 产生该btc的交易的hash |
| `VOUT` | int | btc在交易中的输出索引 |
| `BLOCK_HEIGHT` | int | 交易所在块 |
| `PAYMENT_TYPE` | varchar(100) | btc类型 |
| `PUBKEY_SCRIPT` | varchar(300) | 验签脚本 |
| `cent_amount` | decimal(19) | btc金额 satoshi |
| `OWNER_ADDRESS` | varchar(100) | btc所属钱包地址 |
| `TRANSFER_ORDER_ID` | bigint | id(yyyyMMdd999999999) |
| `CREATED_TIME` | timestamp(3) | 待补 |

## 主键 / 索引
- 主键:`ID`
- `uk_uspt_vout`:TX_HASH, VOUT (UNIQUE)
- `i_tso_ct`:CREATED_TIME

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
