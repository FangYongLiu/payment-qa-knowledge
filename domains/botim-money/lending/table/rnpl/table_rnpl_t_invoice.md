---
id: tbl_rnpl_t_invoice
object_type: Table
name: t_invoice (t_invoice)
aliases: [t_invoice, rnpl.t_invoice]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: rnpl schema DDL
tags: [lending, rnpl]
sensitivity: normal
related_services: []
---

# t_invoice (t_invoice)

## 用途
物理表 `rnpl.t_invoice`,主键 `id`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | 待补 · 可空 |
| `contract_id` | int | rent contract id |
| `payment_id` | int | payment id from t_payment table |
| `file_tag` | varchar(128) | file_tag · 可空 |
| `create_time` | timestamp | created time |
| `update_time` | timestamp | The last update date for the EMI |
| `bill_id` | int | bill id from t_bill table |
| `invoice_no` | varchar(32) | unique invoice number |
| `principle` | decimal(20, 6) | The principal amount |
| `vat_on_principle` | decimal(20, 6) | VAT on principal amount |
| `usage_fee` | decimal(20, 6) | Fee for usage |
| `vat_on_usage` | decimal(20, 6) | VAT on usage fee |
| `late_payment_fee` | decimal(20, 6) | Fee for late payment |
| `vat_on_late_payment_fee` | decimal(20, 6) | VAT on late payment fee |
| `total_before_vat` | decimal(20, 6) | Total amount before VAT |
| `total_vat` | decimal(20, 6) | Total VAT amount |
| `total_payment` | decimal(20, 6) | Total payment amount including VAT |
| `processing_fee` | decimal(20, 2) | Processing fee |
| `vat_on_processing_fee` | decimal(20, 2) | VAT on processing fee |

## 主键 / 索引
- 主键:`id`
- `unique_bill_payment`:bill_id, payment_id (UNIQUE)
- `unique_t_invoice_invoice_no`:invoice_no (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
