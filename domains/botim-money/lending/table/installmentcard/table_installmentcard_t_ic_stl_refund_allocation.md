---
id: tbl_installmentcard_t_ic_stl_refund_allocation
object_type: Table
name: Refund allocation — tracks how refunds are distributed to installments, statement items, or wallet (t_ic_stl_refund_allocation)
aliases: [t_ic_stl_refund_allocation, installmentcard.t_ic_stl_refund_allocation]
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

# Refund allocation — tracks how refunds are distributed to installments, statement items, or wallet (t_ic_stl_refund_allocation)

## 用途
物理表 `installmentcard.t_ic_stl_refund_allocation`,主键 `id`。Refund allocation — tracks how refunds are distributed to installments, statement items, or wallet。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 待补 · 可空 |
| `account_id` | bigint | Account ID |
| `refund_txn_id` | bigint | Refund CardTxn ID — which refund caused this |
| `loan_id` | bigint | Order ID — which loan the refund is against |
| `installment_id` | bigint | Installment ID — NULL for wallet refund · 可空 |
| `statement_id` | bigint | Statement ID — NULL if unbilled · 可空 |
| `statement_item_id` | bigint | Statement item ID — NULL if unbilled or wallet · 可空 |
| `item_type` | tinyint | 0=PRINCIPAL, 1=INTEREST, 2=LPF, 3=LPF_VAT, 4=WALLET_REFUND |
| `allocated_amount` | decimal(18, 2) | Amount allocated |
| `refund_transfer_id` | bigint | PaybyRefundTransfer ID — set for wallet refunds · 可空 |
| `allocation_order` | int | Sequence within this refund |
| `created_at` | datetime | 待补 |

## 主键 / 索引
- 主键:`id`
- `idx_refund_alloc_account`:account_id
- `idx_refund_alloc_installment`:installment_id
- `idx_refund_alloc_loan`:loan_id
- `idx_refund_alloc_refund_txn`:refund_txn_id
- `idx_refund_alloc_statement`:statement_id

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
