---
id: tbl_installmentcard_t_ic_cm_card
object_type: Table
name: Card master: stores card details linked to account. Lifecycle decoupled from installment lifecycle (t_ic_cm_card)
aliases: [t_ic_cm_card, installmentcard.t_ic_cm_card]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: installmentcard schema DDL
tags: [lending, installmentcard]
sensitivity: normal
related_services: []
---

# Card master: stores card details linked to account. Lifecycle decoupled from installment lifecycle (t_ic_cm_card)

## 用途
物理表 `installmentcard.t_ic_cm_card`,主键 `id`。Card master: stores card details linked to account. Lifecycle decoupled from installment lifecycle。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | Primary key · 可空 |
| `account_id` | bigint | Account identifier (logical ref to t_ic_am_account.id, no FK) |
| `member_id` | varchar(32) | External member/customer ID (denormalized, no FK) |
| `card_external_id` | varchar(64) | Unique card ID from PayBy |
| `card_type` | tinyint | Card type: 0=MC |
| `card_status` | tinyint | Card status: 0=ISSUED, 1=ACTIVE, 2=BLOCKED, 3=CLOSED, 4=LOST, 5=REPLACED, 6=EXPIRED |
| `issued_at` | datetime | When card was issued |
| `activated_at` | datetime | When card was activated (nullable) · 可空 |
| `blocked_at` | datetime | When card was blocked (nullable) · 可空 |
| `closed_at` | datetime | When card was closed (nullable) · 可空 |
| `last4` | varchar(4) | Optional last 4 digits for display only · 可空 |
| `expiry_month` | tinyint | Optional expiry month (1-12) · 可空 |
| `expiry_year` | smallint | Optional expiry year (e.g., 2028) · 可空 |
| `created_at` | datetime | Record creation timestamp |
| `updated_at` | datetime | Record last update timestamp |
| `created_by` | varchar(50) | Service/user that created the record |
| `updated_by` | varchar(50) | Service/user that last updated the record |
| `is_deleted` | tinyint | Soft delete flag: 0=false, 1=true |

## 主键 / 索引
- 主键:`id`
- `uk_card_external_id`:card_external_id (UNIQUE)
- `idx_account_id`:account_id
- `idx_member_id`:member_id

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
