---
id: tbl_ccdeposit_t_wallet_address
object_type: Table
name: 钱包地址 (t_wallet_address)
aliases: [t_wallet_address, ccdeposit.t_wallet_address]
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

# 钱包地址 (t_wallet_address)

## 用途
物理表 `ccdeposit.t_wallet_address`,主键 `id`。钱包地址。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | id |
| `chain_code` | varchar(32) | 链代码 |
| `address` | varchar(128) | 充币地址 |
| `wallet_type` | varchar(16) | 钱包类型 MEMBER CUSTOMER |

## 主键 / 索引
- 主键:`id`
- `uk_wa_addr`:chain_code, address (UNIQUE)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
