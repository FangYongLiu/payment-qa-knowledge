---
id: tbl_rnpl_t_pmc
object_type: Table
name: Property Management Company master table (t_pmc)
aliases: [t_pmc, rnpl.t_pmc]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: rnpl schema DDL
tags: [lending, rnpl]
sensitivity: normal
related_services: []
---

# Property Management Company master table (t_pmc)

## 用途
物理表 `rnpl.t_pmc`,主键 `pmc_id`。Property Management Company master table。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `pmc_id` | int | System-generated unique ID of a PMC · 可空 |
| `company_name` | varchar(128) | Name of the Property Management Company |
| `contact_person_name` | varchar(200) | Full name of the contact person · 可空 |
| `contact_person_title` | varchar(200) | Title/designation of the contact person · 可空 |
| `contact_person_phone` | varchar(20) | Phone number of the contact person · 可空 |
| `contact_person_email` | varchar(255) | Email address of the contact person · 可空 |
| `communication_phone` | varchar(20) | General communication phone number · 可空 |
| `communication_email` | varchar(255) | General communication email address · 可空 |
| `payby_merchant_id` | varchar(64) | PayBy wallet merchant ID · 可空 |
| `iban_number` | varchar(64) | Bank IBAN number for payments · 可空 |
| `bank_name` | varchar(128) | Bank name associated with IBAN · 可空 |
| `start_date` | timestamp | Date from which PMC is active for RNPL · 可空 |
| `end_date` | timestamp | Date from which PMC is deactivated for RNPL · 可空 |
| `status` | tinyint(2) | Status of the PMC: 1=active, 0=inactive, 2=suspended · 可空 |
| `created_at` | timestamp | Record creation timestamp · 可空 |
| `updated_at` | timestamp | Record update timestamp |

## 主键 / 索引
- 主键:`pmc_id`
- 无(仅主键)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
