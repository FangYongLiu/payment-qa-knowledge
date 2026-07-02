---
id: tbl_mhtfundout_t_fundout_bankcard_beneficiary
object_type: Table
name: 出款到银行卡子表 (t_fundout_bankcard_beneficiary)
aliases: [t_fundout_bankcard_beneficiary, mhtfundout.t_fundout_bankcard_beneficiary]
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

# 出款到银行卡子表 (t_fundout_bankcard_beneficiary)

## 用途
物理表 `mhtfundout.t_fundout_bankcard_beneficiary`,主键 `id`。出款到银行卡子表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | id |
| `full_name_ues_token` | varchar(200) | 姓名uestoken · 可空 |
| `full_name_sha256_hex` | varchar(200) | 姓名摘要 · 可空 |
| `iban_ues_token` | varchar(200) | iban uestoken · 可空 |
| `iban_sha256_hex` | varchar(200) | iban摘要 · 可空 |
| `swift_code` | varchar(200) | swift code · 可空 |
| `iban_mask_text` | varchar(200) | iban掩码 · 可空 |
| `full_name_mask_text` | varchar(200) | 姓名掩码 · 可空 |
| `address_ues_token` | varchar(200) | 地址uestoken · 可空 |
| `address_sha256_hex` | varchar(200) | 地址摘要 · 可空 |
| `address_mask_text` | varchar(200) | 地址掩码 · 可空 |
| `account_no_sha256_hex` | varchar(200) | 地址uestoken · 可空 |
| `account_no_ues_token` | varchar(32) | 地址摘要 · 可空 |
| `account_no_mask_text` | varchar(64) | 地址掩码 · 可空 |
| `bank_name` | varchar(128) | 银行名称 · 可空 |
| `country_code` | varchar(8) | 国家代码 · 可空 |
| `fundout_crcy_code` | varchar(8) | fundoutCurrencyCode · 可空 |
| `fedwire_code` | varchar(16) | fedwireCode · 可空 |
| `intermediary_bank` | varchar(16) | intermediaryBank · 可空 |
| `branch_name` | varchar(128) | branchName · 可空 |
| `beneficiary_type` | varchar(16) | beneficiaryType · 可空 |
| `city_code` | varchar(8) | cityCode · 可空 |
| `purpose_code` | varchar(16) | purposeCode · 可空 |
| `beneficiary_post_code` | varchar(8) | Postal Code of the beneficiary · 可空 |
| `account_holder_type` | varchar(16) | Type of account holder such as Individual or Business · 可空 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
