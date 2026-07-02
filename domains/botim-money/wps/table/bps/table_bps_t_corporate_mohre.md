---
id: tbl_bps_t_corporate_mohre
object_type: Table
name: Table to store corporate data from Mohre (t_corporate_mohre)
aliases: [t_corporate_mohre, bps.t_corporate_mohre]
domain: wps
status: active
owner: xinwei.cao
reviewer: xinwei.cao
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: bps schema DDL
tags: [wps, bps]
sensitivity: normal
related_services: []
---

# Table to store corporate data from Mohre (t_corporate_mohre)

## 用途
物理表 `bps.t_corporate_mohre`,主键 `id`。Table to store corporate data from Mohre。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | char(32) | identifier for the corporate entity |
| `mohre_registration_number` | varchar(32) | MOHRE registration number · 可空 |
| `mohre_status` | varchar(16) | MOHRE status · 可空 |
| `mohre_licence_place` | varchar(32) | Place of MOHRE licence · 可空 |
| `mohre_licence_number` | varchar(32) | MOHRE licence number · 可空 |
| `mohre_company_code` | varchar(32) | MOHRE company code · 可空 |
| `compliance_status` | varchar(16) | Compliance status is optional · 可空 |
| `last_salary_info` | varchar(500) | Last salary information · 可空 |
| `owner_name_ar` | varchar(100) | Owner name in Arabic · 可空 |
| `owner_name` | varchar(100) | Owner name · 可空 |
| `passport_no` | varchar(16) | Passport number · 可空 |
| `emirates_id` | varchar(32) | Emirates ID · 可空 |
| `person_mol_id` | varchar(32) | Person MOL ID · 可空 |
| `company_name` | varchar(100) | Company name · 可空 |
| `company_name_ar` | varchar(100) | Company name in Arabic · 可空 |
| `unified_number` | varchar(32) | Unified number · 可空 |
| `create_at` | timestamp | Record creation timestamp · 可空 |
| `update_at` | timestamp | Last update timestamp · 可空 |
| `mohre_license_place_ar` | varchar(32) | Place of MOHRE license in arabic · 可空 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
