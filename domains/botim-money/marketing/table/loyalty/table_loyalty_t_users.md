---
id: tbl_loyalty_t_users
object_type: Table
name: User records linked to Talon.One customer profiles (t_users)
aliases: [t_users, loyalty.t_users]
domain: marketing
status: active
owner: wujiang.ding
reviewer: wujiang.ding
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: loyalty schema DDL
tags: [marketing, loyalty]
sensitivity: normal
related_services: []
---

# User records linked to Talon.One customer profiles (t_users)

## 用途
物理表 `loyalty.t_users`,主键 `id`。User records linked to Talon.One customer profiles。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint unsigned | Primary key auto-increment · 可空 |
| `integration_id` | varchar(105) | BigData user ID - used as Talon.One integrationId (format: ab:v1:<sha256>, ~70 chars) |
| `ucid` | varchar(50) | Unique customer ID from Botim platform |
| `payby_mid` | varchar(20) | PayBy member ID for payment integration · 可空 |
| `created_source` | varchar(10) | How user record was created: bigdata|api|event (bigdata=T+1 sync with full attributes, api=Day 1 user via API with valid JWT, event=real-time event before BigData sync) |
| `kyc_status` | varchar(50) | KYC status from BigData (e.g., KYC Verified, Not Verified) · 可空 |
| `first_kyc_date` | timestamp | When KYC was first completed · 可空 |
| `nationality` | varchar(50) | User nationality from KYC (e.g., INDIA, PAKISTAN, PHILIPPINES) · 可空 |
| `age` | tinyint unsigned | User age in years · 可空 |
| `gender` | varchar(10) | User gender: Male|Female|Other · 可空 |
| `vip_status` | varchar(20) | VIP status: non_vip, vip, etc. · 可空 |
| `remittance_count_lifetime` | int unsigned | Total number of remittances (imt_transaction_count_lifetime) · 可空 |
| `remittance_amount_lifetime` | decimal(15, 2) | Total amount remitted in AED (imt_transaction_amount_lifetime) · 可空 |
| `first_remittance_at` | timestamp | Date of first remittance (first_remittance_transaction_date) · 可空 |
| `first_name` | varchar(50) | User first name from BigData · 可空 |
| `country_code` | varchar(10) | Country code (e.g., AE, IN, PK, PH) · 可空 |
| `device_language` | varchar(20) | Device language setting (e.g., en, ar, hi) · 可空 |
| `ip_region` | varchar(50) | Region derived from IP address · 可空 |
| `country` | varchar(50) | Country name (e.g., United Arab Emirates, India) · 可空 |
| `platform` | varchar(20) | Mobile platform: iOS, Android · 可空 |
| `current_app_version` | varchar(50) | Current app version installed · 可空 |
| `email` | varchar(100) | User email (lowercased, ≤100 chars) — backfilled from BigData; consumed by MoEngage Content API · 可空 |
| `phone_number` | varchar(20) | User phone in E.164 format — backfilled from BigData; consumed by MoEngage Content API · 可空 |
| `talon_profile_created_at` | timestamp | When profile was first created in Talon.One · 可空 |
| `talon_profile_synced_at` | timestamp | Last successful sync with Talon.One · 可空 |
| `bigdata_synced_at` | timestamp | Last sync of profile data from BigData · 可空 |
| `needs_talon_sync` | tinyint(1) | Flag indicating user needs Talon.One sync (TRUE: new/updated user, FALSE: synced) |
| `created_at` | timestamp | Record creation timestamp |
| `updated_at` | timestamp | Record last update timestamp |
| `inventory_sync_due_at` | timestamp | Scheduled time for delayed inventory sync (set after event processing) · 可空 |
| `inventory_synced_at` | timestamp | Last successful inventory sync completion (for 24h counter) · 可空 |

## 主键 / 索引
- 主键:`id`
- `uk_users_integration_id`:integration_id (UNIQUE)
- `uk_users_ucid`:ucid (UNIQUE)
- `idx_users_inventory_sync_due`:inventory_sync_due_at
- `idx_users_needs_sync`:needs_talon_sync

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
