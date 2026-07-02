---
id: tbl_salarynow_t_pre_assessed_risk
object_type: Table
name: Pre-assessed risk data for employees (t_pre_assessed_risk)
aliases: [t_pre_assessed_risk, salarynow.t_pre_assessed_risk]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: salarynow schema DDL
tags: [lending, salarynow]
sensitivity: normal
related_services: []
---

# Pre-assessed risk data for employees (t_pre_assessed_risk)

## 用途
物理表 `salarynow.t_pre_assessed_risk`,主键 `id`。Pre-assessed risk data for employees。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int(20) | Primary key · 可空 |
| `member_id` | varchar(20) | Member identifier from user profile |
| `company_id` | varchar(64) | Company identifier |
| `company_name` | varchar(128) | Company name |
| `corporate_registration_id` | varchar(64) | Corporate registration identifier · 可空 |
| `employee_id` | varchar(32) | Employee identifier |
| `employee_name` | varchar(128) | Employee name |
| `nationality` | varchar(64) | Employee nationality |
| `botim_status` | varchar(8) | Botim status flag · 可空 |
| `risk_tier` | varchar(32) | Risk tier: High, Medium, Low |
| `monthly_salary_aed` | decimal(10, 2) | Monthly salary in AED |
| `monthly_salary_range` | int | Monthly salary range category · 可空 |
| `salary_continuity` | int | Salary continuity in months |
| `uae_phone_flag` | varchar(8) | UAE phone flag: Yes, No |
| `delinquency_flag` | varchar(8) | Delinquency flag: Yes, No |
| `outstanding_loan_flag` | varchar(8) | Outstanding loan flag: Yes, No |
| `wps_outstanding_loan_flag` | varchar(8) | WPS outstanding loan flag: Yes, No · 可空 |
| `eligible_flag` | varchar(8) | Eligible flag: Y, N |
| `max_limit_aed` | decimal(10, 2) | Maximum limit in AED |
| `allowed_tenors` | varchar(64) | Allowed tenors as JSON array |
| `tenor_1m_limit_aed` | decimal(10, 2) | 1 month tenor limit in AED · 可空 |
| `tenor_2m_limit_aed` | decimal(10, 2) | 2 month tenor limit in AED · 可空 |
| `tenor_3m_limit_aed` | decimal(10, 2) | 3 month tenor limit in AED · 可空 |
| `dbr_cap_percent` | decimal(10, 2) | DBR cap percentage |
| `matrix_version` | varchar(32) | Risk matrix version · 可空 |
| `create_time` | timestamp | Record creation timestamp |
| `update_time` | timestamp | Last update timestamp |

## 主键 / 索引
- 主键:`id`
- `uk_pre_assessed_risk_company_employee`:company_id, employee_id (UNIQUE)
- `uk_pre_assessed_risk_member_id`:member_id (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
