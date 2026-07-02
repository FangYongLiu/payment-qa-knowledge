---
id: tbl_ppc_t_transaction_order
object_type: Table
name: Transaction Order (t_transaction_order)
aliases: [t_transaction_order, ppc.t_transaction_order]
domain: card
status: active
owner: jianfei.wang
reviewer: jianfei.wang
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: ppc schema DDL
tags: [card, ppc]
sensitivity: normal
related_services: []
---

# Transaction Order (t_transaction_order)

## 用途
物理表 `ppc.t_transaction_order`,主键 `trx_voucher_no`。Transaction Order。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `trx_voucher_no` | bigint | Transaction Voucher Number |
| `orig_trx_voucher_no` | bigint | Original Transaction Voucher Number · 可空 |
| `reversal_trx_voucher_no` | bigint | Reversal Transaction Voucher Number · 可空 |
| `transaction_type` | varchar(10) | Transaction Type: T-Pending, R-Reversals, S-Settled, RL-Released, CB-Chargeback, F-Fee, RF-Fee Reversal, FRL-Fee Release, P-Pre Auth Completion, C-Clearing · 可空 |
| `txn_code` | varchar(10) | Transaction Code · 可空 |
| `channel_type` | varchar(10) | Values include: POS、ECOM、ATM · 可空 |
| `virtual_card_id` | bigint | Virtual Card ID |
| `drcr_indicator` | char | DrCr Indicator: D-Debit, C-Credit |
| `spend_mode` | char | D-for Debit Card,C-for Credit Card · 可空 |
| `wallet_amount` | decimal(19, 4) | Total Wallet Amount |
| `wallet_currency` | char(3) | Wallet Currency |
| `reverse_auth_amount` | decimal(19, 4) | Reverse Auth Amount · 可空 |
| `transaction_status` | varchar(10) | Transaction Status: W-Waiting, P-Processing, F-Failure, S-Success, RW-Retry Waiting, YF-YSE Failure |
| `transaction_detail` | varchar(255) | Transaction Detail: [{"type":"P","code":"010000","amount":"0.01"}] |
| `local_txn_detail` | varchar(255) | Local Txn Detail · 可空 |
| `actual_detail` | varchar(255) | Actual Detail · 可空 |
| `actual_local_detail` | varchar(255) | Actual Local Detail · 可空 |
| `crs_detail` | varchar(255) | Crs Detail · 可空 |
| `payment_voucher_no` | bigint | Payment Voucher Number · 可空 |
| `biz_product_code` | varchar(10) | Biz Product Code · 可空 |
| `bill_flag` | char | Bill Flag: Y-Yes · 可空 |
| `unity_result_code` | varchar(50) | Unity Result Code · 可空 |
| `extension` | varchar(255) | Extension · 可空 |
| `create_time` | timestamp | Create Time |
| `update_time` | timestamp | Update Time |

## 主键 / 索引
- 主键:`trx_voucher_no`
- `idx_card_id_transaction_status`:virtual_card_id, transaction_status
- `idx_orig_trx_voucher_no`:orig_trx_voucher_no
- `idx_payment_order_no`:payment_voucher_no
- `idx_reversal_trx_voucher_no`:reversal_trx_voucher_no
- `idx_update_time_card_id`:update_time, virtual_card_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
