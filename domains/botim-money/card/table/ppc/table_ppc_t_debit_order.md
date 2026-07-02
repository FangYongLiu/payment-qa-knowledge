---
id: tbl_ppc_t_debit_order
object_type: Table
name: Debit Order (t_debit_order)
aliases: [t_debit_order, ppc.t_debit_order]
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

# Debit Order (t_debit_order)

## 用途
物理表 `ppc.t_debit_order`,主键 `debit_voucher_no`。Debit Order。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `debit_voucher_no` | bigint | Debit Voucher Number |
| `txn_ref_no` | varchar(32) | Txn Ref No: Unique Transaction Reference |
| `virtual_card_id` | bigint | Virtual Card ID |
| `drcr_indicator` | char(2) | DrCr Indicator: D-Debit |
| `debit_type` | varchar(3) | Debit Type: FEE-Charge the fee |
| `transaction_code` | char(4) | Transaction Code |
| `amount` | decimal(19, 4) | Amount |
| `currency` | char(3) | Currency |
| `debit_status` | varchar(10) | Debit Status: P-Processing;S-Success;F-Failure;WR-Wait Retry; |
| `product_code` | varchar(6) | Product Code |
| `payment_voucher_no` | bigint | Payment Voucher No · 可空 |
| `remarks` | varchar(250) | Remarks · 可空 |
| `create_time` | timestamp | Create Time |
| `update_time` | timestamp | Update Time |

## 主键 / 索引
- 主键:`debit_voucher_no`
- `idx_txn_ref_no`:txn_ref_no
- `idx_update_time_card_id`:update_time, virtual_card_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
