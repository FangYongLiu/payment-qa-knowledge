---
id: tbl_bps_t_payroll_paf_detail
object_type: Table
name: payroll paf detail info (t_payroll_paf_detail)
aliases: [t_payroll_paf_detail, bps.t_payroll_paf_detail]
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

# payroll paf detail info (t_payroll_paf_detail)

## 用途
物理表 `bps.t_payroll_paf_detail`,主键 `id`。payroll paf detail info。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | char(32) | primary key |
| `payroll_paf_id` | char(32) | payroll paf id |
| `request_ref_number` | varchar(64) | request ref number |
| `employee_mol_id` | varchar(64) | employee mol id |
| `first_name` | varchar(125) | first name |
| `last_name` | varchar(125) | last name |
| `iban` | varchar(32) | iban |
| `salary_amount` | varchar(16) | salary amount |
| `pay_start_date` | varchar(16) | pay start date |
| `pay_end_date` | varchar(16) | pay end date |
| `days_in_period` | varchar(16) | days in period |
| `income_fixed` | varchar(16) | income fixed |
| `income_variable` | varchar(16) | income variable |
| `days_on_leave` | varchar(16) | days on leave |
| `branch_id` | varchar(64) | branch id |
| `status` | varchar(10) | status |
| `createAt` | timestamp | create time |
| `updateAt` | timestamp | update time |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
