---
id: tbl_credit_t_cs_credit_pre_audit_record
object_type: Table
name: user credit pre audit record (t_cs_credit_pre_audit_record)
aliases: [t_cs_credit_pre_audit_record, credit.t_cs_credit_pre_audit_record]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: credit schema DDL
tags: [lending, credit]
sensitivity: normal
related_services: []
---

# user credit pre audit record (t_cs_credit_pre_audit_record)

## 用途
物理表 `credit.t_cs_credit_pre_audit_record`,主键 `id`。user credit pre audit record。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int(11) | id · 可空 |
| `product_code` | varchar(10) | product code |
| `application_id` | varchar(45) | application Id · 可空 |
| `user_id` | varchar(20) | user ID |
| `income` | varchar(100) | income · 可空 |
| `income_precisely` | varchar(20) | precisely income · 可空 |
| `salary_date` | varchar(3) | salary date · 可空 |
| `has_credit_card` | tinyint(1) | has credit card（1=yes，0=no） · 可空 |
| `living_expense` | varchar(100) | living expense · 可空 |
| `living_expense_precisely` | varchar(20) | precisely living expense · 可空 |
| `created_time` | timestamp | created time · 可空 |
| `last_modified` | timestamp | last modified · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_application_id`:application_id
- `idx_user_id`:user_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
