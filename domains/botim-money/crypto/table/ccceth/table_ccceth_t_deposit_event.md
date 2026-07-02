---
id: tbl_ccceth_t_deposit_event
object_type: Table
name: 转账事件(分区) (t_deposit_event)
aliases: [t_deposit_event, ccceth.t_deposit_event]
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

# 转账事件(分区) (t_deposit_event)

## 用途
物理表 `ccceth.t_deposit_event`,主键 `id`。转账事件(分区)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | id |
| `event_usage` | varchar(50) | 用途 · 可空 |
| `ignored` | varchar(50) | 是否被忽略 |
| `chain_code` | varchar(32) | 待补 |
| `category` | varchar(32) | 事件类型 |
| `currency_code` | varchar(32) | 提币币种 |
| `amount` | decimal(23, 8) | 充值金额 |
| `cent_amount` | decimal(32) | 原始充值金额 |
| `payer_address` | varchar(200) | 付款人地址 |
| `receiver_address` | varchar(200) | 收款人地址 |
| `block_number` | bigint | 待补 |
| `tx_hash` | varchar(200) | 事务hash |
| `created_time` | timestamp(3) | 创建时间 |

## 主键 / 索引
- 主键:`id`
- `i_de_bn`:block_number
- `i_de_ct`:created_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
