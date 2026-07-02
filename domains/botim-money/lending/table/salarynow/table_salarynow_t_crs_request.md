---
id: tbl_salarynow_t_crs_request
object_type: Table
name: Capital Recovery Service requests - enables multiple payment transactions per bill (t_crs_request)
aliases: [t_crs_request, salarynow.t_crs_request]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: salarynow schema DDL
tags: [lending, salarynow]
sensitivity: normal
related_services: []
---

# Capital Recovery Service requests - enables multiple payment transactions per bill (t_crs_request)

## 用途
物理表 `salarynow.t_crs_request`,主键 `id`。Capital Recovery Service requests - enables multiple payment transactions per bill。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | Primary key · 可空 |
| `bill_id` | bigint | Reference to t_loan_bill.id |
| `sent_amount` | decimal(10, 2) | Amount sent for collection via CRS |
| `paid_amount` | decimal(10, 2) | Amount actually paid/collected |
| `pay_status` | varchar(20) | Payment status: PENDING, PARTIAL_PAID, PAID, FAILED |
| `paid_at` | timestamp | Timestamp when payment was completed · 可空 |
| `created_at` | timestamp | Creation timestamp |
| `updated_at` | timestamp | Last update timestamp |

## 主键 / 索引
- 主键:`id`
- `idx_crs_request_bill_id`:bill_id
- `idx_crs_request_status`:pay_status

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
