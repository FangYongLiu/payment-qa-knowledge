---
id: tbl_npss_t_debit_reverse_order
object_type: Table
name: Debit reverse order table (t_debit_reverse_order)
aliases: [t_debit_reverse_order, npss.t_debit_reverse_order]
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: npss schema DDL
tags: [payment-core, npss]
sensitivity: normal
related_services: []
---

# Debit reverse order table (t_debit_reverse_order)

## 用途
物理表 `npss.t_debit_reverse_order`,主键 `reverse_voucher_no`。Debit reverse order table。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `reverse_voucher_no` | bigint | Reverse voucher number |
| `pre_voucher_no` | bigint | Previous debit voucher number (related to t_debit_order) · 可空 |
| `reverse_type` | varchar(10) | Reverse transaction type · 可空 |
| `merchant_id` | varchar(20) | Merchant ID · 可空 |
| `member_id` | varchar(20) | Member ID · 可空 |
| `amount` | varchar(32) | Amount |
| `currency` | char(3) | Currency |
| `status` | varchar(10) | Status |
| `id_sct` | varchar(32) | Bank order number (transactionId) |
| `merchant_trx_id` | varchar(32) | Merchant transaction ID · 可空 |
| `cdtr_bic` | varchar(11) | Creditor bank BIC · 可空 |
| `dbtr_bic` | varchar(11) | Debtor bank BIC · 可空 |
| `reverse_category` | varchar(20) | Reverse category · 可空 |
| `response_code` | varchar(10) | Response code · 可空 |
| `unity_result_code` | varchar(20) | Unity result code · 可空 |
| `extension` | varchar(512) | Extension parameters · 可空 |
| `memo` | varchar(255) | Memo/Reason · 可空 |
| `gmt_create` | timestamp(3) | Create time |
| `gmt_modified` | timestamp(3) | Modify time · 可空 |
| `gmt_finished` | timestamp(3) | Finish time · 可空 |

## 主键 / 索引
- 主键:`reverse_voucher_no`
- `uk_reverse_idsct`:id_sct (UNIQUE)
- `idx_reverse_merchant_id`:merchant_id, gmt_modified

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
