---
id: tbl_bps_t_sif_status_record
object_type: Table
name: sif status record (t_sif_status_record)
aliases: [t_sif_status_record, bps.t_sif_status_record]
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

# sif status record (t_sif_status_record)

## 用途
物理表 `bps.t_sif_status_record`,主键 `id`。sif status record。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | char(32) | primary key |
| `origin_id` | varchar(64) | origin id |
| `sif_file_id` | varchar(64) | sif file id |
| `sif_file_name` | varchar(255) | sif file name |
| `corporate_registration_id` | varchar(32) | corporate molid |
| `employee_registration_id` | varchar(32) | employee registration id |
| `routing_code` | varchar(16) | routing code · 可空 |
| `iban` | varchar(32) | iban |
| `income_fixed` | decimal(11, 2) | income fixed |
| `income_variable` | decimal(11, 2) | income variable |
| `days_on_leave` | varchar(8) | days on leave |
| `salary_month` | varchar(16) | salary month |
| `transfer_mode` | varchar(16) | transfer mode |
| `error_code` | varchar(10) | error code |
| `error_message` | varchar(255) | error message · 可空 |
| `createAt` | timestamp | create time |
| `updateAt` | timestamp | update time |
| `payroll_start_date` | char(10) | payroll start date · 可空 |
| `payroll_end_date` | char(10) | payroll end date · 可空 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
