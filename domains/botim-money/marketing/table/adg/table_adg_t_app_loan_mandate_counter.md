---
id: tbl_adg_t_app_loan_mandate_counter
object_type: Table
name: Mandate counter againist each loan (t_app_loan_mandate_counter)
aliases: [t_app_loan_mandate_counter, adg.t_app_loan_mandate_counter]
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

# Mandate counter againist each loan (t_app_loan_mandate_counter)

## 用途
物理表 `adg.t_app_loan_mandate_counter`,主键 `id`。Mandate counter againist each loan。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | primary key · 可空 |
| `app_code` | varchar(31) | Client application code |
| `loan_id` | varchar(63) | Loan ID choosen by client appication. Expected Integer or uuid |
| `mandate_count` | int | Serialized Mandate count for a single loan |

## 主键 / 索引
- 主键:`id`
- `uk_app_code_loan_id`:app_code, loan_id (UNIQUE)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
