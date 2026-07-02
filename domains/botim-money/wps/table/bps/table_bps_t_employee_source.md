---
id: tbl_bps_t_employee_source
object_type: Table
name: Employee original information for upload (t_employee_source)
aliases: [t_employee_source, bps.t_employee_source]
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

# Employee original information for upload (t_employee_source)

## 用途
物理表 `bps.t_employee_source`,主键 `id`。Employee original information for upload。业务语义细节**待补**(表结构来自 DDL)。

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
| `staff_id` | varchar(32) | staff id · 可空 |
| `employee_registration_id` | varchar(100) | employee MOL ID · 可空 |
| `first_name` | varchar(250) | first name · 可空 |
| `last_name` | varchar(250) | last name · 可空 |
| `dob` | varchar(16) | dob · 可空 |
| `gender` | varchar(10) | gender · 可空 |
| `nationality` | varchar(64) | nationality · 可空 |
| `eid_number` | varchar(100) | eid number · 可空 |
| `eid_expiry` | varchar(100) | eid expiry · 可空 |
| `passport_number` | varchar(100) | passport number · 可空 |
| `mobile_no` | varchar(16) | mobile no · 可空 |
| `salary_loading_IBAN` | varchar(32) | IBAN Number · 可空 |
| `bank_name` | varchar(32) | bank name · 可空 |
| `salary` | decimal(11, 2) | salary · 可空 |
| `request_type` | varchar(32) | request type |
| `occupation` | varchar(100) | Employee occupation · 可空 |
| `validate_result` | varchar(10) | validate result · 可空 |
| `reason` | varchar(255) | reason · 可空 |
| `maker_id` | varchar(64) | maker id |
| `merchant_mid` | char(32) | merchant mid |
| `branch_id` | char(32) | branch id · 可空 |
| `createAt` | timestamp | create time |
| `updateAt` | timestamp | update time |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
