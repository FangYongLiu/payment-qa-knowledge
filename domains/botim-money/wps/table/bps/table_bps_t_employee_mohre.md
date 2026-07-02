---
id: tbl_bps_t_employee_mohre
object_type: Table
name: Table to store employee data from Mohre (t_employee_mohre)
aliases: [t_employee_mohre, bps.t_employee_mohre]
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

# Table to store employee data from Mohre (t_employee_mohre)

## 用途
物理表 `bps.t_employee_mohre`,主键 `id`。Table to store employee data from Mohre。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | char(32) | identifier for the mohre employee |
| `corporate_registration_id` | varchar(32) | Corporate registration ID |
| `unified_number` | varchar(32) | Unified number for the employee |
| `card_number` | int | Card number associated with the employee |
| `salary` | decimal(11, 2) | Salary of the employee |
| `employee_status` | varchar(16) | Status of the employee |
| `passport` | varchar(16) | Passport number of the employee · 可空 |
| `emirates_id` | varchar(32) | Emirates ID of the employee · 可空 |
| `employee_full_name` | varchar(100) | Full name of the employee |
| `employee_full_name_ar` | varchar(100) | Full name of the employee in Arabic |
| `person_code` | varchar(35) | Person code timestamp |
| `status_dated` | timestamp | Status dated timestamp |
| `created_at` | timestamp | Record creation timestamp |
| `updated_at` | timestamp | Last update timestamp |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
