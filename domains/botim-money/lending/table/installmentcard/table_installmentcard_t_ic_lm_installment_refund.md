---
id: tbl_installmentcard_t_ic_lm_installment_refund
object_type: Table
name: t_ic_lm_installment_refund (t_ic_lm_installment_refund)
aliases: [t_ic_lm_installment_refund, installmentcard.t_ic_lm_installment_refund]
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

# t_ic_lm_installment_refund (t_ic_lm_installment_refund)

## 用途
物理表 `installmentcard.t_ic_lm_installment_refund`,主键 `id`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | Unique record ID for installment-refund mapping · 可空 |
| `loan_id` | bigint | Associated loan ID |
| `refund_txn_id` | bigint | Refund transaction ID that triggered this adjustment |
| `old_installment_id` | bigint | Original installment record that was cancelled or settled by the refund |
| `new_installment_id` | bigint | Replacement installment record created after refund adjustment; NULL if fully settled with no replacement · 可空 |
| `installment_no` | int | Installment sequence number within the loan |
| `action` | tinyint | Refund action type: 6=REFUND_SETTLED, 7=REFUND_CANCELLED |
| `principal_settled` | decimal(18, 2) | Principal amount absorbed/settled by this refund |
| `original_principal` | decimal(18, 2) | Original principal amount of the affected installment before refund adjustment · 可空 |
| `original_interest` | decimal(18, 2) | Original interest amount of the affected installment before refund adjustment · 可空 |
| `original_opening` | decimal(18, 2) | Original opening balance of the affected installment before refund adjustment · 可空 |
| `original_closing` | decimal(18, 2) | Original closing balance of the affected installment before refund adjustment · 可空 |
| `created_at` | datetime | Record creation timestamp · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_loan_id`:loan_id
- `idx_refund_txn_id`:refund_txn_id

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
