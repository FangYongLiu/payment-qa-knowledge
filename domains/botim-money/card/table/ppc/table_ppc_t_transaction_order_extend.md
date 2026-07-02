---
id: tbl_ppc_t_transaction_order_extend
object_type: Table
name: Transaction Order Extend (t_transaction_order_extend)
aliases: [t_transaction_order_extend, ppc.t_transaction_order_extend]
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

# Transaction Order Extend (t_transaction_order_extend)

## 用途
物理表 `ppc.t_transaction_order_extend`,主键 `trx_voucher_no`。Transaction Order Extend。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `trx_voucher_no` | bigint | Transaction Voucher Number |
| `ref_number` | varchar(50) | Ref Number: Transaction no from YSE |
| `reversal_ref_number` | varchar(50) | Reversal Ref Number · 可空 |
| `rr_number` | varchar(50) | RRNumber: Transaction no from MasterCard · 可空 |
| `txn_ref_no` | varchar(32) | Txn Ref No: Request no from YSE · 可空 |
| `transaction_type` | varchar(10) | Transaction Type: T-Pending, R-Reversals, S-Settled, RL-Released, CB-Chargeback, F-Fee, RF-Fee Reversal, FRL-Fee Release, P-Pre Auth Completion, C-Clearing · 可空 |
| `proxy_number` | varchar(32) | Proxy Number |
| `transaction_amount` | decimal(19, 4) | Transaction Amount: From Mastercard |
| `transaction_currency` | char(3) | Transaction Currency |
| `billing_amount` | decimal(19, 4) | Billing Amount: From Mastercard |
| `billing_currency` | char(3) | Billing Currency |
| `exchange_rate` | decimal(10, 4) | Exchange Rate |
| `wallet_product_code` | varchar(6) | Wallet Product Code · 可空 |
| `wallet_account` | varchar(12) | Wallet Account: From YSE · 可空 |
| `auth_id` | varchar(6) | Auth ID · 可空 |
| `pos_entry_mode` | char(4) | Authentication Type: CNP, Magstripe, PIN etc · 可空 |
| `system_trace_number` | varchar(8) | System Trace Number · 可空 |
| `opening_wallet_balance` | decimal(19, 4) | Opening Wallet Balance |
| `closing_wallet_balance` | decimal(19, 4) | Closing Wallet Balance · 可空 |
| `token_id` | bigint | Token ID · 可空 |
| `merchant_id` | varchar(50) | Merchant ID · 可空 |
| `merchant_name` | varchar(100) | Merchant Name · 可空 |
| `terminal_id` | varchar(20) | Terminal ID · 可空 |
| `mcc_code` | char(4) | Mcc Code: Merchant Category Code · 可空 |
| `merchant_country_code` | char(4) | Merchant Country Code · 可空 |
| `scheme_code` | varchar(20) | JAYWAN / MASTERCARD · 可空 |
| `remarks` | varchar(100) | Remarks · 可空 |
| `extension` | varchar(255) | Extension · 可空 |
| `processor_time` | timestamp | Processor Time: YSE time |
| `create_time` | timestamp | Create Time |
| `update_time` | timestamp | Update Time |

## 主键 / 索引
- 主键:`trx_voucher_no`
- `idx_ref_number`:ref_number
- `idx_rr_number`:rr_number
- `idx_txn_ref_no`:txn_ref_no
- `idx_update_time`:update_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
