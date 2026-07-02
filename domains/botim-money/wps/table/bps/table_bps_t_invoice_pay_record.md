---
id: tbl_bps_t_invoice_pay_record
object_type: Table
name: invoice pay record (t_invoice_pay_record)
aliases: [t_invoice_pay_record, bps.t_invoice_pay_record]
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

# invoice pay record (t_invoice_pay_record)

## 用途
物理表 `bps.t_invoice_pay_record`,主键 `id`。invoice pay record。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | char(32) | primary key |
| `trade_request_no` | varchar(64) | trade request no |
| `refund_request_no` | varchar(64) | refund request no · 可空 |
| `invoice_no` | varchar(64) | invoice number |
| `invoice_type` | varchar(16) | invoice type |
| `amount` | decimal(11, 2) | invoice amount |
| `trade_product_code` | varchar(16) | trade product code |
| `trade_status` | char(2) | trade status |
| `message` | varchar(255) | message · 可空 |
| `maker_id` | varchar(100) | maker id |
| `createAt` | timestamp | create time |
| `updateAt` | timestamp | update time |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
