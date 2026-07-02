---
id: tbl_bps_t_payroll_source_data
object_type: Table
name: Payroll original information (t_payroll_source_data)
aliases: [t_payroll_source_data, bps.t_payroll_source_data]
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

# Payroll original information (t_payroll_source_data)

## 用途
物理表 `bps.t_payroll_source_data`,主键 `id`。Payroll original information。业务语义细节**待补**(表结构来自 DDL)。

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
| `income_total` | decimal(11, 2) | income total |
| `income_fixed` | decimal(11, 2) | income fixed |
| `income_variable` | decimal(11, 2) | income variable · 可空 |
| `transfer_mode` | varchar(16) | transfer mode · 可空 |
| `staff_id` | varchar(64) | staff id · 可空 |
| `first_name` | varchar(125) | first name |
| `last_name` | varchar(125) | last name |
| `pay_start_date` | varchar(16) | pay start date · 可空 |
| `pay_end_date` | varchar(16) | pay end date · 可空 |
| `employer_id` | varchar(16) | employer id · 可空 |
| `days_on_leave` | int | days on leave · 可空 |
| `routing_code` | varchar(32) | routing code · 可空 |
| `employee_registration_id` | varchar(100) | employee MOL ID · 可空 |
| `eid_number` | varchar(32) | eid number · 可空 |
| `eid_expiry` | varchar(32) | eid expiry · 可空 |
| `iban` | varchar(32) | iban · 可空 |
| `bank_name` | varchar(100) | bank name · 可空 |
| `salary` | decimal(11, 2) | salary |
| `employee_type` | varchar(16) | employee type |
| `salary_loading_date` | timestamp | salary loading date · 可空 |
| `status` | varchar(16) | status |
| `reason` | varchar(255) | reason · 可空 |
| `maker_id` | varchar(64) | maker id |
| `approver_id` | varchar(64) | approver id |
| `branch_mol_id` | varchar(64) | 待补 · 可空 |
| `merchant_mid` | char(32) | merchant mid |
| `remarks` | varchar(250) | remarks · 可空 |
| `createAt` | timestamp | create time |
| `updateAt` | timestamp | update time |
| `total_benefits` | decimal(11, 2) | additional benefit apart from salary · 可空 |
| `total_deductions` | decimal(11, 2) | deductions from salary · 可空 |
| `total_allowances` | decimal(11, 2) | additional allowances · 可空 |
| `total_incentives` | decimal(11, 2) | incentives · 可空 |
| `income_breakdown` | text | variable income breakdown json string · 可空 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
