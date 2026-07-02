---
id: tbl_ccdeposit_t_customer_wallet
object_type: Table
name: 客户钱包 (t_customer_wallet)
aliases: [t_customer_wallet, ccdeposit.t_customer_wallet]
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

# 客户钱包 (t_customer_wallet)

## 用途
物理表 `ccdeposit.t_customer_wallet`,主键 `id`。客户钱包。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | id |
| `address` | varchar(128) | 充币地址 |
| `chain_code` | varchar(32) | 链代码 |
| `member_id` | varchar(32) | 用户MID |
| `customer_id` | varchar(200) | 链代码 |
| `created_time` | timestamp(3) | 创建时间 |

## 主键 / 索引
- 主键:`id`
- `uk_cw_custm`:customer_id, chain_code, member_id (UNIQUE)
- `uk_cw_mc`:chain_code, address (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
