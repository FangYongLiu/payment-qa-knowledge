---
id: tbl_botimsnpl_t_sl_extension
object_type: Table
name: t_sl_extension (t_sl_extension)
aliases: [t_sl_extension, botimsnpl.t_sl_extension]
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

# t_sl_extension (t_sl_extension)

## 用途
物理表 `botimsnpl.t_sl_extension`,主键 `id`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 待补 · 可空 |
| `user_id` | varchar(20) | user id |
| `bill_id` | int | bill id |
| `bill_no` | varchar(64) | bill no |
| `extension_config_id` | bigint | extension config id |
| `extension_days` | int | Days extended (e.g. 7) |
| `original_due_date` | timestamp | Original due date before extension |
| `new_due_date` | timestamp | New due date after extension |
| `unpaid_principal` | decimal(15, 2) | Unpaid principal at time of extension |
| `fee_amount` | decimal(15, 2) | Extension fee (excl. VAT) |
| `vat_amount` | decimal(15, 2) | VAT amount |
| `total_fee` | decimal(15, 2) | Total fee (incl. VAT) |
| `pay_record_id` | int(10) | id in repay_record · 可空 |
| `status` | smallint | 0=Pending 1=Success 2=Failed |
| `ext` | varchar(255) | ext · 可空 |
| `is_read` | smallint | 0-unread, 1-read |
| `created_time` | timestamp | created time |
| `last_modified` | timestamp | last modified time |

## 主键 / 索引
- 主键:`id`
- `idx_extension_bill_id`:bill_id
- `idx_extension_bill_no`:bill_no
- `idx_extension_config_id`:extension_config_id
- `idx_extension_created_time`:created_time
- `idx_extension_user_id`:user_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
