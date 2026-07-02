---
id: tbl_ccceth_t_crypto_wallet
object_type: Table
name: 数字钱包(分区,根据address hash) (t_crypto_wallet)
aliases: [t_crypto_wallet, ccceth.t_crypto_wallet]
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

# 数字钱包(分区,根据address hash) (t_crypto_wallet)

## 用途
物理表 `ccceth.t_crypto_wallet`,主键 `id`。数字钱包(分区,根据address hash)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | id |
| `address` | varchar(200) | 钱包地址(分区) |
| `credential` | varchar(200) | 私钥 |
| `encryption_type` | varchar(50) | 密钥加密方式 |
| `deposit_enabled` | varchar(50) | 是否开启充值 |
| `wallet_owner` | varchar(50) | 所属 · 可空 |
| `wallet_usage` | varchar(50) | 用途 · 可空 |
| `created_time` | timestamp(3) | 创建时间 |
| `last_updated_time` | timestamp(3) | 最后更新时间 |
| `data_version` | bigint | 数据版本 |

## 主键 / 索引
- 主键:`id`
- `uk_cw_addr`:address (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **乐观锁**:更新须带 `data_version`,并发校验版本递增。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
