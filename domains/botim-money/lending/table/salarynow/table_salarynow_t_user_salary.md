---
id: tbl_salarynow_t_user_salary
object_type: Table
name: Stores salary records of users, mapped to user_profile (t_user_salary)
aliases: [t_user_salary, salarynow.t_user_salary]
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

# Stores salary records of users, mapped to user_profile (t_user_salary)

## 用途
物理表 `salarynow.t_user_salary`,主键 `id`。Stores salary records of users, mapped to user_profile。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | Primary key · 可空 |
| `member_id` | varchar(20) | Reference to user_profile.member_id |
| `salary_month` | char(7) | Salary month in format MM-YYYY |
| `fixed_income` | decimal(10, 2) | Fixed component of salary |
| `variable_income` | decimal(10, 2) | Variable component like bonus or commission · 可空 |
| `total_income` | decimal(10, 2) | Sum of fixed and variable income · 可空 |
| `process_datetime` | timestamp | Date and time salary was processed (UAE time) |
| `notes` | varchar(255) | Any remarks or additional info about the salary · 可空 |
| `create_time` | timestamp | Record creation timestamp · 可空 |
| `last_modified` | timestamp | Last update timestamp · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_user_salary_member_id`:member_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
