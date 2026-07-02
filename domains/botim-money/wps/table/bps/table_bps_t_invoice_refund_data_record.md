---
id: tbl_bps_t_invoice_refund_data_record
object_type: Table
name: invoice refund data record (t_invoice_refund_data_record)
aliases: [t_invoice_refund_data_record, bps.t_invoice_refund_data_record]
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

# invoice refund data record (t_invoice_refund_data_record)

## 用途
物理表 `bps.t_invoice_refund_data_record`,主键 `id`。invoice refund data record。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | char(32) | primary key |
| `corporate_id` | varchar(32) | corporate id |
| `corporate_name` | varchar(200) | corporate name |
| `trade_request_no` | varchar(32) | trade request no |
| `refund_request_no` | varchar(32) | refund request no |
| `origin_bulk_id` | varchar(32) | origin bulk id |
| `origin_bulk_type` | varchar(16) | origin bulk type |
| `invoice_id` | varchar(32) | invoice id |
| `invoice_type` | varchar(16) | invoice type |
| `amount` | decimal(11, 2) | amount |
| `product_code` | varchar(16) | product code |
| `status` | varchar(16) | status |
| `message` | varchar(100) | message · 可空 |
| `createAt` | timestamp | create time |
| `updateAt` | timestamp | update time |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
