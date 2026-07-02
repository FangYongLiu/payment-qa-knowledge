---
id: tbl_adg_t_credit_details
object_type: Table
name: Stores credit and payment details related to loans (t_credit_details)
aliases: [t_credit_details, adg.t_credit_details]
domain: marketing
status: active
owner: wujiang.ding
reviewer: wujiang.ding
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: adg schema DDL
tags: [marketing, adg]
sensitivity: normal
related_services: []
---

# Stores credit and payment details related to loans (t_credit_details)

## 用途
物理表 `adg.t_credit_details`,主键 `id`。Stores credit and payment details related to loans。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | Unique identifier, primary key · 可空 |
| `app_code` | varchar(31) | Application code |
| `user_id` | varchar(63) | User identifier |
| `loan_id` | varchar(63) | Loan identifier |
| `min_pay_amount` | decimal(10, 4) | Minimum payment amount · 可空 |
| `max_pay_amount` | decimal(10, 4) | Maximum payment amount · 可空 |
| `start_date` | date | Payment schedule start date · 可空 |
| `end_date` | date | Payment schedule end date · 可空 |
| `payment_frequency` | varchar(63) | Frequency of payment (e.g., monthly, weekly) · 可空 |
| `create_time` | timestamp | Record creation timestamp |
| `update_time` | timestamp | Record last update timestamp |

## 主键 / 索引
- 主键:`id`
- `uk_app_code_user_id_loan_id`:app_code, user_id, loan_id (UNIQUE)
- `idx_app_code_loan_id`:app_code, loan_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
