---
id: tbl_bps_t_branch_corporate_source_data
object_type: Table
name: Branch corporate registration data records (t_branch_corporate_source_data)
aliases: [t_branch_corporate_source_data, bps.t_branch_corporate_source_data]
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

# Branch corporate registration data records (t_branch_corporate_source_data)

## 用途
物理表 `bps.t_branch_corporate_source_data`,主键 `id`。Branch corporate registration data records。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | char(32) | ULID primary key |
| `origin_id` | varchar(32) | Original record ID from Excel |
| `origin_bulk_id` | varchar(32) | Reference to bulk ID |
| `branch_id` | varchar(64) | Branch MOL ID / Corporate Registration ID |
| `branch_name` | varchar(255) | Branch corporate name |
| `country` | varchar(100) | Country |
| `city` | varchar(50) | City |
| `address` | varchar(100) | Address |
| `area` | varchar(100) | Area/District · 可空 |
| `trade_license_number` | varchar(64) | Trade license number |
| `trade_license_expiry_date` | varchar(16) | Trade license expiry date |
| `contact_person_name` | varchar(64) | Contact person name |
| `contact_person_email` | varchar(64) | Contact person email |
| `contact_person_phone` | varchar(20) | Contact person phone · 可空 |
| `contact_person_mobile_phone` | varchar(50) | Contact person mobile |
| `contact_person_eid` | varchar(50) | Contact person Emirates ID |
| `company_established_date` | varchar(16) | Company established date · 可空 |
| `exchange_house_onboarding_date` | varchar(16) | Exchange house onboarding date · 可空 |
| `status` | varchar(10) | Record status: Normal, Failed, Completed, Processing |
| `reason` | varchar(255) | Error reason if status is Failed · 可空 |
| `maker_id` | varchar(32) | User who created the record |
| `createAt` | timestamp | Created timestamp |
| `updateAt` | timestamp | Updated timestamp |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
