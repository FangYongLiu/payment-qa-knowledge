---
id: tbl_installmentcard_t_ic_cm_wallet_command
object_type: Table
name: Executed wallet commands per transaction (t_ic_cm_wallet_command)
aliases: [t_ic_cm_wallet_command, installmentcard.t_ic_cm_wallet_command]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: installmentcard schema DDL
tags: [lending, installmentcard]
sensitivity: normal
related_services: []
---

# Executed wallet commands per transaction (t_ic_cm_wallet_command)

## 用途
物理表 `installmentcard.t_ic_cm_wallet_command`,主键 `id`。Executed wallet commands per transaction。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 待补 · 可空 |
| `txn_id` | bigint | FK to t_ic_cm_card_txn |
| `trx_voucher_no` | varchar(64) | Transaction voucher number |
| `command_sequence` | int | Execution order (1, 2, 3...) |
| `command_type` | varchar(10) | F, U, UD, D, C |
| `wallet_amount` | decimal(18, 2) | Command amount |
| `currency` | varchar(3) | Currency code · 可空 |
| `executed_at` | datetime | When command was executed |
| `created_at` | datetime | 待补 · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_trx_voucher_no`:trx_voucher_no
- `idx_txn_id`:txn_id

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
