---
id: tbl_ccceth_t_wallet_nonce
object_type: Table
name: 钱包nonce(分区) (t_wallet_nonce)
aliases: [t_wallet_nonce, ccceth.t_wallet_nonce]
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

# 钱包nonce(分区) (t_wallet_nonce)

## 用途
物理表 `ccceth.t_wallet_nonce`,主键 `id`。钱包nonce(分区)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 通用指令id |
| `nonce` | bigint | 钱包nonce |
| `block_number` | bigint | 块高 · 可空 |
| `created_time` | timestamp(3) | 创建时间 |
| `address` | varchar(200) | 钱包地址(分区) |

## 主键 / 索引
- 主键:`id`
- `uk_wlt_nc`:nonce, address (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
