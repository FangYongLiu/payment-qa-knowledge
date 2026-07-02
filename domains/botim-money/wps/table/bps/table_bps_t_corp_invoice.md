---
id: tbl_bps_t_corp_invoice
object_type: Table
name: corporate invoice (t_corp_invoice)
aliases: [t_corp_invoice, bps.t_corp_invoice]
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

# corporate invoice (t_corp_invoice)

## 用途
物理表 `bps.t_corp_invoice`,主键 `id`。corporate invoice。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | varchar(32) | ulid |
| `invoice_no` | varchar(32) | invoice no |
| `merchant_id` | varchar(32) | merchant id |
| `merchant_info_id` | varchar(32) | merchant info id |
| `invoice_type` | varchar(20) | invoice type |
| `payment_model` | varchar(20) | payment model |
| `charge_code` | varchar(10) | charge code |
| `vat` | decimal(19, 4) | vat |
| `total` | decimal(19, 4) | total amount |
| `sub_total` | decimal(19, 4) | sub total |
| `vat_amount` | decimal(19, 4) | vat amount |
| `payment_date` | timestamp | payment date · 可空 |
| `invoice_date` | timestamp | invoice date · 可空 |
| `month` | varchar(15) | month |
| `year` | varchar(4) | year |
| `status` | varchar(20) | status |
| `create_at` | timestamp | create time · 可空 |
| `update_at` | timestamp | update time · 可空 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
