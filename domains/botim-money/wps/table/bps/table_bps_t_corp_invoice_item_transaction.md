---
id: tbl_bps_t_corp_invoice_item_transaction
object_type: Table
name: corporate invoice item transaction (t_corp_invoice_item_transaction)
aliases: [t_corp_invoice_item_transaction, bps.t_corp_invoice_item_transaction]
domain: wps
status: active
owner: xinwei.cao
reviewer: xinwei.cao
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: bps schema DDL
tags: [wps, bps]
sensitivity: normal
related_services: []
---

# corporate invoice item transaction (t_corp_invoice_item_transaction)

## 用途
物理表 `bps.t_corp_invoice_item_transaction`,主键 `id`。corporate invoice item transaction。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | varchar(32) | ulid |
| `invoice_id` | varchar(32) | invoice id |
| `trxn_id` | varchar(32) | transaction id |
| `trxn_type` | varchar(30) | transaction type |
| `trxn_title` | varchar(100) | transaction title |
| `trxn_date` | timestamp | transaction date · 可空 |
| `trxn_memo` | varchar(255) | transaction memo |
| `unit_amount` | decimal(19, 4) | unit amount |
| `create_at` | timestamp | create time · 可空 |
| `update_at` | timestamp | update time · 可空 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
