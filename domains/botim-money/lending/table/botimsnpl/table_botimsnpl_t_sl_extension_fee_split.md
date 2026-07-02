---
id: tbl_botimsnpl_t_sl_extension_fee_split
object_type: Table
name: t_sl_extension_fee_split (t_sl_extension_fee_split)
aliases: [t_sl_extension_fee_split, botimsnpl.t_sl_extension_fee_split]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: botimsnpl schema DDL
tags: [lending, botimsnpl]
sensitivity: normal
related_services: []
---

# t_sl_extension_fee_split (t_sl_extension_fee_split)

## 用途
物理表 `botimsnpl.t_sl_extension_fee_split`,主键 `id`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | 待补 · 可空 |
| `extension_id` | int | FK to t_sl_extension |
| `pay_record_id` | int(10) | id in repay_record · 可空 |
| `ins_id` | int | FK to t_sl_instalment |
| `order_no` | varchar(64) | Order number |
| `split_fee` | decimal(15, 2) | Split fee amount (incl. VAT) · 可空 |
| `split_fee_excl_vat` | decimal(15, 2) | Split fee amount (excl. VAT) · 可空 |
| `split_vat` | decimal(15, 2) | Split VAT amount · 可空 |
| `refund_status` | smallint | 0=Not refunded, 1=Refunded · 可空 |
| `ext` | varchar(255) | ext · 可空 |
| `created_time` | timestamp | created time |
| `last_modified` | timestamp | last modified time |

## 主键 / 索引
- 主键:`id`
- `idx_extension_split_bill_no`:order_no
- `idx_extension_split_created_time`:created_time
- `idx_extension_split_extension_id`:extension_id
- `idx_extension_split_ins_id`:ins_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
