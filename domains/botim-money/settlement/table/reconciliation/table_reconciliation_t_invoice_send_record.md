---
id: tbl_reconciliation_t_invoice_send_record
object_type: Table
name: Invoice sending records (t_invoice_send_record)
aliases: [t_invoice_send_record, reconciliation.t_invoice_send_record]
domain: settlement
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: reconciliation schema DDL
tags: [settlement, reconciliation]
sensitivity: normal
related_services: []
---

# Invoice sending records (t_invoice_send_record)

## 用途
物理表 `reconciliation.t_invoice_send_record`,主键 `invoice_id`。Invoice sending records。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `invoice_id` | bigint | Invoice Record ID |
| `fund_channel_code` | varchar(32) | Channel Code |
| `biz_type` | varchar(4) | Business Type |
| `bill_date` | varchar(10) | Transaction Date |
| `due_date` | varchar(10) | Operate Date · 可空 |
| `total_amount` | decimal(19, 4) | Transaction total amount · 可空 |
| `fund_total_amount` | decimal(19, 4) | Fund total amount · 可空 |
| `commission_charge` | decimal(19, 4) | Commission charges deducted · 可空 |
| `charge_rate` | decimal(10, 6) | Commission charges deducted Rate · 可空 |
| `vat` | decimal(19, 4) | VAT commission deducted · 可空 |
| `vat_rate` | decimal(10, 6) | VAT commission deducted Rate · 可空 |
| `net_amount` | decimal(19, 4) | Net amount to be settled · 可空 |
| `init_total_amount` | decimal(19, 4) | Total amount of initial fund amount · 可空 |
| `result` | char | Sending Result: S-success F-fail · 可空 |
| `failed_reason` | varchar(500) | Failed Reason · 可空 |
| `operator` | varchar(45) | Account of operator · 可空 |
| `send_time` | timestamp | Send Time · 可空 |

## 主键 / 索引
- 主键:`invoice_id`
- 无(仅主键)

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
