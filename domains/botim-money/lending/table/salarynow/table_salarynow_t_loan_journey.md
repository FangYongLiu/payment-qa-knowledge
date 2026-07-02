---
id: tbl_salarynow_t_loan_journey
object_type: Table
name: Audit trail for all events related to a loan application (t_loan_journey)
aliases: [t_loan_journey, salarynow.t_loan_journey]
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

# Audit trail for all events related to a loan application (t_loan_journey)

## 用途
物理表 `salarynow.t_loan_journey`,主键 `id`。Audit trail for all events related to a loan application。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | Primary key · 可空 |
| `member_id` | varchar(20) | payby id for the user also primary key |
| `journey_name` | varchar(64) | Name of the event (NEW, OFFER_INITIATED, LOAN_OFFERED, etc.) |
| `journey_name_desc` | varchar(64) | Name of the sub journey event. |
| `ref_id` | varchar(32) | References loan offer, loan application, loan number, disbursement ref etc |
| `performed_by` | varchar(64) | who performed the action, how it has been performed · 可空 |
| `remarks` | varchar(128) | Optional notes or metadata for the event · 可空 |
| `event_time` | timestamp | When the event occurred · 可空 |
| `created_at` | timestamp | Record creation time |
| `updated_at` | timestamp | Record last update time |

## 主键 / 索引
- 主键:`id`
- `idx_loan_journey_member_id`:member_id

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
