---
id: tbl_fts_tr_fts_fim_order
object_type: Table
name: tr_fts_fim_order (tr_fts_fim_order)
aliases: [tr_fts_fim_order, fts.tr_fts_fim_order]
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

# tr_fts_fim_order (tr_fts_fim_order)

## 用途
物理表 `fts.tr_fts_fim_order`,主键 `id`。tr_fts_fim_order。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | unique ID · 可空 |
| `file_order_no` | varchar(32) | unique no |
| `filename` | varchar(32) | filename like E035413C1031032402270092291.FTR |
| `source` | char(3) |  from 2nd to 4th in the file name. remitter bank code.like 035 |
| `message_type` | char(5) | message like O103N |
| `sequence_number` | char(6) | sequence number in file,increment. like 000001 |
| `beneficiary_institution_identifier` | varchar(16) | beneficiary institution identifier like S/E413AEXX |
| `transaction_type_code` | char(3) | transaction type code like MWO/FIS… |
| `valid_date` | char(6) | valid date fomatter:YYMMDD |
| `currency_code` | char(3) | currency code like AED |
| `settled_transaction_amount` | decimal(19, 2) | settled transaction amount |
| `instructed_amount` | decimal(19, 2) | instructed amount |
| `ordering_customer_type` | char(5) | ordering customer type like 0904/ |
| `ordering_customer_account` | varchar(35) | ordering customer account, regular is an IBAN |
| `ordering_customer_info` | varchar(140) | Ordering Customer Name & Address,PAYBY TECHNOLOGY PROJECTS LLC P.O BoxPO BOX,112778 RGP BUILDING 48 ABU DHABI UAE AE · 可空 |
| `ordering_institution` | varchar(140) | ordering institution like N/NBAD |
| `beneficiary_account` | varchar(80) | beneficiary account like CA IBAN, PAYBY V IBAN, PPC |
| `beneficiary_info` | varchar(128) | Beneficiary Account Name & Address:PayBy Technologies Project LLC · 可空 |
| `remittance_info` | varchar(140) | remittance info · 可空 |
| `charges` | char(3) | OUR |
| `reference_no` | varchar(16) | NFR/24/006494131 |
| `fts_id` | varchar(30) | last 16 of filename 1032402270092291 |
| `extension` | varchar(255) | backup · 可空 |
| `status` | char | I,S,F,R · 可空 |
| `state` | varchar(20) | INIT，FUND_PROCESSING，FUND_SUCCESS，FUND_FAIL，PENDING（OTHER TYPE），REFUND_SUCCESS，REFUND_FAIL，REFUND_PROCESSING · 可空 |
| `gmt_create` | timestamp | create time |
| `gmt_update` | timestamp | update time |
| `is_compensate` | char | 0:no need to compensate,1:need to compensate · 可空 |
| `order_type` | varchar(12) | order type · 可空 |
| `ccn_batch_no` | varchar(32) | ccn batch no · 可空 |

## 主键 / 索引
- 主键:`id`
- `udx_tffo_fon`:file_order_no (UNIQUE)
- `idx_tffo_cbn`:ccn_batch_no
- `idx_tffo_gct`:gmt_create

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
