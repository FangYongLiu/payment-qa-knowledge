---
id: tbl_installmentcard_t_ic_lm_loan_adjustment
object_type: Table
name: t_ic_lm_loan_adjustment (t_ic_lm_loan_adjustment)
aliases: [t_ic_lm_loan_adjustment, installmentcard.t_ic_lm_loan_adjustment]
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

# t_ic_lm_loan_adjustment (t_ic_lm_loan_adjustment)

## 用途
物理表 `installmentcard.t_ic_lm_loan_adjustment`,主键 `id`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 待补 · 可空 |
| `loan_id` | bigint | Loan being adjusted |
| `account_id` | bigint | Account ID (denormalized) |
| `adjustment_txn_id` | bigint | Refund/chargeback transaction ID |
| `trx_voucher_no` | varchar(64) | Transaction voucher number |
| `adjustment_type` | tinyint | 1=PARTIAL_REFUND, 2=FULL_REFUND, 3=CHARGEBACK |
| `adjustment_reason` | varchar(255) | adjustment_reason · 可空 |
| `adjustment_amount` | decimal(18, 2) | Total wallet credit amount |
| `principal_adjusted` | decimal(18, 2) | principal_adjusted |
| `interest_adjusted` | decimal(18, 2) | interest_adjusted |
| `loan_status_before` | tinyint | loan_status_before |
| `loan_status_after` | tinyint | loan_status_after |
| `replacement_loan_id` | bigint | If partial refund, new loan created with reduced amount · 可空 |
| `created_at` | datetime(3) | created_at |
| `created_by` | varchar(50) | created_by |

## 主键 / 索引
- 主键:`id`
- `uk_adjustment_txn_id`:adjustment_txn_id (UNIQUE)
- `uk_trx_voucher_no`:trx_voucher_no (UNIQUE)
- `idx_account_id`:account_id
- `idx_loan_id`:loan_id

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
