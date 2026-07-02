---
id: tbl_bps_t_employee_source_data
object_type: Table
name: Employee original information (t_employee_source_data)
aliases: [t_employee_source_data, bps.t_employee_source_data]
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

# Employee original information (t_employee_source_data)

## 用途
物理表 `bps.t_employee_source_data`,主键 `id`。Employee original information。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | char(32) | primary key |
| `origin_id` | varchar(64) | unique num |
| `origin_bulk_id` | varchar(64) | batch num |
| `staff_id` | varchar(32) | staff id |
| `employee_registration_id` | varchar(100) | employee MOL ID · 可空 |
| `first_name` | varchar(250) | first name |
| `middle_name` | varchar(64) | middle name · 可空 |
| `last_name` | varchar(250) | last name |
| `mother_name` | varchar(100) | mother name · 可空 |
| `dob` | varchar(16) | dob |
| `gender` | varchar(10) | gender |
| `title` | varchar(64) | title · 可空 |
| `nationality` | varchar(64) | nationality |
| `address1` | varchar(255) | address1 · 可空 |
| `address2` | varchar(255) | address2 · 可空 |
| `address3` | varchar(255) | address3 · 可空 |
| `address4` | varchar(255) | address4 · 可空 |
| `city` | varchar(64) | city · 可空 |
| `state` | varchar(64) | state · 可空 |
| `country` | varchar(32) | country · 可空 |
| `postcode` | varchar(32) | postcode · 可空 |
| `phone_no` | varchar(16) | phone no · 可空 |
| `eid_number` | varchar(100) | eid number · 可空 |
| `eid_expiry` | varchar(100) | eid expiry · 可空 |
| `passport_number` | varchar(20) | passport number · 可空 |
| `mobile_no` | varchar(16) | mobile no |
| `email_address` | varchar(64) | email address · 可空 |
| `name_on_card` | varchar(256) | name on card · 可空 |
| `salary_loading_IBAN` | varchar(32) | IBAN Number · 可空 |
| `routing_code` | varchar(32) | routing code · 可空 |
| `salary` | decimal(11, 2) | salary |
| `employee_type` | varchar(16) | employee type |
| `status` | varchar(20) | status |
| `request_type` | varchar(32) | request type |
| `have_issue_card` | char(6) | have issue card · 可空 |
| `reason` | varchar(255) | reason · 可空 |
| `document_type` | varchar(16) | document type:Eid,Passport,Evisa · 可空 |
| `front_file_id` | char(32) | front file id · 可空 |
| `back_file_id` | char(32) | back file id · 可空 |
| `merchant_mid` | char(32) | merchant mid |
| `parent_merchant_mid` | varchar(64) | parent merchant mid · 可空 |
| `occupation` | varchar(100) | Employee occupation · 可空 |
| `maker_id` | varchar(64) | maker id |
| `approver_id` | varchar(64) | approver id · 可空 |
| `createAt` | timestamp | create time |
| `updateAt` | timestamp | update time |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
