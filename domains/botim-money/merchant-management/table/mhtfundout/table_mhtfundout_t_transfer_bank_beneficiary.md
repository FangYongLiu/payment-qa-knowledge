---
id: tbl_mhtfundout_t_transfer_bank_beneficiary
object_type: Table
name: t_transfer_bank_beneficiary (t_transfer_bank_beneficiary)
aliases: [t_transfer_bank_beneficiary, mhtfundout.t_transfer_bank_beneficiary]
domain: merchant-management
status: active
owner: yijian.tan
reviewer: yijian.tan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: mhtfundout schema DDL
tags: [merchant-management, mhtfundout]
sensitivity: normal
related_services: []
---

# t_transfer_bank_beneficiary (t_transfer_bank_beneficiary)

## 用途
物理表 `mhtfundout.t_transfer_bank_beneficiary`,主键 `id`。t_transfer_bank_beneficiary。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | global id |
| `card_number_ues_token` | varchar(32) | card_number_ues_token |
| `card_number_sha256_hex` | varchar(128) | card_number_sha256_hex |
| `card_number_mask_text` | varchar(64) | card_number_mask_text |
| `expiry_month` | varchar(32) | expiry_month |
| `expiry_year` | varchar(32) | expiry_year |
| `account_holder_type` | varchar(16) | account holder type |
| `first_name_ues_token` | varchar(32) | first_name_ues_token · 可空 |
| `first_name_sha256_hex` | varchar(128) | first_name_sha256_hex · 可空 |
| `first_name_mask_text` | varchar(64) | first_name_mask_text · 可空 |
| `last_name_ues_token` | varchar(32) | last_name_ues_token · 可空 |
| `last_name_sha256_hex` | varchar(128) | last_name_sha256_hex · 可空 |
| `last_name_mask_text` | varchar(64) | last_name_mask_text · 可空 |
| `middle_name_ues_token` | varchar(32) | middle_name_ues_token · 可空 |
| `middle_name_sha256_hex` | varchar(128) | middle_name_sha256_hex · 可空 |
| `middle_name_mask_text` | varchar(64) | middle_name_mask_text · 可空 |
| `company_name_ues_token` | varchar(32) | company_name_ues_token · 可空 |
| `company_name_sha256_hex` | varchar(128) | company_name_sha256_hex · 可空 |
| `company_name_mask_text` | varchar(64) | company_name_mask_text · 可空 |
| `created_time` | timestamp(3) | created_time |
| `country_code` | varchar(8) | countryCode · 可空 |
| `region` | varchar(8) | region · 可空 |
| `zip_code` | varchar(16) | zipCode · 可空 |
| `city` | varchar(64) | city · 可空 |
| `card_token` | varchar(64) | cardToken · 可空 |
| `address_line` | varchar(128) | address_line · 可空 |
| `card_token_mid` | varchar(32) | cardTokenMerchantId · 可空 |

## 主键 / 索引
- 主键:`id`
- `i_tbb_ct`:created_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
