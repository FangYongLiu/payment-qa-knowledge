---
id: tbl_bps_t_corp_invoice_fee_code
object_type: Table
name: corporate invoice fee code (t_corp_invoice_fee_code)
aliases: [t_corp_invoice_fee_code, bps.t_corp_invoice_fee_code]
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

# corporate invoice fee code (t_corp_invoice_fee_code)

## 用途
物理表 `bps.t_corp_invoice_fee_code`,主键 `id`。corporate invoice fee code。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | varchar(32) | ulid |
| `business_line` | varchar(32) | business line |
| `charge_code` | varchar(10) | charge code |
| `segment_category` | varchar(2) | segment category |
| `payment_method` | varchar(20) | payment method |
| `invoice_vat` | decimal(19, 4) | invoice vat |
| `status` | varchar(10) | status |
| `create_at` | timestamp | create time · 可空 |
| `update_at` | timestamp | update time · 可空 |
| `invoicing_model` | varchar(25) | MONTHLY INVOICING MODEL |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
