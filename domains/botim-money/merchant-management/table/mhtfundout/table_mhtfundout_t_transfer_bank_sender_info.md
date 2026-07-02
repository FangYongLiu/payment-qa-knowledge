---
id: tbl_mhtfundout_t_transfer_bank_sender_info
object_type: Table
name: t_transfer_bank_sender_info (t_transfer_bank_sender_info)
aliases: [t_transfer_bank_sender_info, mhtfundout.t_transfer_bank_sender_info]
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

# t_transfer_bank_sender_info (t_transfer_bank_sender_info)

## 用途
物理表 `mhtfundout.t_transfer_bank_sender_info`,主键 `id`。t_transfer_bank_sender_info。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | global id |
| `first_name_ues_token` | varchar(32) | first_name_ues_token · 可空 |
| `first_name_sha256_hex` | varchar(128) | first_name_sha256_hex · 可空 |
| `first_name_mask_text` | varchar(64) | first_name_mask_text · 可空 |
| `last_name_ues_token` | varchar(32) | last_name_ues_token · 可空 |
| `last_name_sha256_hex` | varchar(128) | last_name_sha256_hex · 可空 |
| `last_name_mask_text` | varchar(64) | last_name_mask_text · 可空 |
| `created_time` | timestamp(3) | created_time |
| `country_code` | varchar(8) | countryCode · 可空 |
| `region` | varchar(8) | region · 可空 |
| `zip_code` | varchar(16) | zipCode · 可空 |
| `city` | varchar(64) | city · 可空 |
| `address_line` | varchar(128) | address line · 可空 |
| `source_of_funds` | varchar(64) | sourceOfFunds · 可空 |
| `reference` | varchar(64) | reference · 可空 |
| `date_of_birth` | varchar(10) | dateOfBirth · 可空 |

## 主键 / 索引
- 主键:`id`
- `i_tbb_ct`:created_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
