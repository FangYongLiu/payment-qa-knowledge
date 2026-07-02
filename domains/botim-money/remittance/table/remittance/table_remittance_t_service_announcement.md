---
id: tbl_remittance_t_service_announcement
object_type: Table
name: Service announcements (banner config) (t_service_announcement)
aliases: [t_service_announcement, remittance.t_service_announcement]
domain: remittance
status: active
owner: lei.pan
reviewer: lei.pan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: remittance schema DDL
tags: [remittance, remittance]
sensitivity: normal
related_services: []
---

# Service announcements (banner config) (t_service_announcement)

## 用途
物理表 `remittance.t_service_announcement`,主键 `id`。Service announcements (banner config)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint unsigned | Primary Key · 可空 |
| `internal_label` | varchar(200) | Internal label, ops-only, not shown to users |
| `target_country` | varchar(8) | Receiving country code (ISO alpha-2). Single value, required |
| `target_currency` | varchar(8) | Receiving currency code (ISO 4217). Single value, required |
| `transfer_method` | varchar(32) | BANK_TRANSFER/MOBILE_WALLET/CASH_PICK_UP/UPI. NULL = all methods · 可空 |
| `title` | varchar(200) | Announcement title shown in the banner |
| `description` | varchar(600) | Full announcement body shown on tap |
| `lang_type` | char(3) | Authoring language of title/description; reserved for future per-language rows |
| `start_time` | timestamp | Effective start time (UTC; compared against app-passed timestamp) |
| `end_time` | timestamp | Effective end time (UTC; compared against app-passed timestamp) |
| `status` | char | Enable kill-switch (Y/N). Lifecycle is time-driven; N hard-hides |
| `created_by` | varchar(64) | Creator (admin account) |
| `modified_by` | varchar(64) | Last modifier (admin account) |
| `gmt_create` | timestamp | Creation timestamp |
| `gmt_modified` | timestamp | Last modification timestamp |

## 主键 / 索引
- 主键:`id`
- `idx_target_country_currency`:target_country, target_currency

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
