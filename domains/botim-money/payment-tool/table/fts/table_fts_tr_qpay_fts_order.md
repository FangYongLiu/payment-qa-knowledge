---
id: tbl_fts_tr_qpay_fts_order
object_type: Table
name: fund transfer CTO (tr_qpay_fts_order)
aliases: [tr_qpay_fts_order, fts.tr_qpay_fts_order]
domain: payment-tool
status: active
owner: kingo.liang
reviewer: kingo.liang
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: fts schema DDL
tags: [payment-tool, fts]
sensitivity: normal
related_services: []
---

# fund transfer CTO (tr_qpay_fts_order)

## 用途
物理表 `fts.tr_qpay_fts_order`,主键 `id`。fund transfer CTO。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 唯一标识符 · 可空 |
| `batch_no` | varchar(16) | 批次编号 |
| `source` | varchar(30) | 系统来源 |
| `record_type` | varchar(10) | 待补 · 可空 |
| `transaction_type` | char | B,S |
| `source_reference` | varchar(32) | 待补 |
| `message_type_identifier` | varchar(30) | I001N,I103N,I202N · 可空 |
| `sequence_number` | char(6) | 6 digitals · 可空 |
| `currency_code` | char(3) | AED |
| `valid_date` | char(10) | YYMMDD |
| `transaction_amount` | decimal(19, 2) | 交易金额 |
| `settled_transaction_amount` | decimal(19, 2) | 已结算交易金额 · 可空 |
| `reference_no` | varchar(16) | 参考号 |
| `related_reference_no` | varchar(64) | CB202 use · 可空 |
| `fts_transaction_type` | char(8) | CB202 use · 可空 |
| `payer_type` | varchar(32) | CB103 use · 可空 |
| `payer_id` | varchar(32) | payer id · 可空 |
| `payer_name` | varchar(128) | CB001 use · 可空 |
| `payer_address` | varchar(128) | CB103 use · 可空 |
| `payer_account` | varchar(32) | CB103 use · 可空 |
| `payee_id` | varchar(32) | CB202 use · 可空 |
| `payee_name` | varchar(128) | CB103 use · 可空 |
| `payee_address` | varchar(128) | CB103 use · 可空 |
| `payee_account` | varchar(32) | CB202 use · 可空 |
| `pay_in_mode` | char(3) | CB001 use · 可空 |
| `remittance_information` | varchar(140) | CB103 use · 可空 |
| `details_of_charges` | char(3) | CB103 use · 可空 |
| `future_use` | char(6) | UAEFTS |
| `extension` | varchar(1024) | back · 可空 |
| `status` | char | I,S,F |
| `gmt_create` | timestamp | 创建时间 |
| `gmt_update` | timestamp | 修改时间 |
| `ori_sequence_number` | char(6) | ccn need · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_batch_no`:batch_no
- `idx_order_source`:source, source_reference

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
