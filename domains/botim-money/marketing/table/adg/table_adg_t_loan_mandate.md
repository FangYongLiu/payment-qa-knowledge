---
id: tbl_adg_t_loan_mandate
object_type: Table
name: Stores loan mandate mapping information, including DDA reference and usage status (t_loan_mandate)
aliases: [t_loan_mandate, adg.t_loan_mandate]
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

# Stores loan mandate mapping information, including DDA reference and usage status (t_loan_mandate)

## 用途
物理表 `adg.t_loan_mandate`,主键 `id`。Stores loan mandate mapping information, including DDA reference and usage status。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | Unique identifier, primary key · 可空 |
| `app_code` | varchar(63) | Application code |
| `user_id` | varchar(63) | User identifier |
| `loan_id` | varchar(63) | Loan identifier |
| `dda_reference_number` | varchar(127) | DDA reference number · 可空 |
| `is_in_use` | tinyint(1) | Flag indicating if the mandate is currently in use (0 = false, 1 = true) |
| `is_next_candidate` | tinyint(1) | Flag indicating if the mandate is the next candidate for use (0 = false, 1 = true) |
| `create_time` | timestamp | Record creation timestamp |
| `update_time` | timestamp | Record last update timestamp |

## 主键 / 索引
- 主键:`id`
- `idx_app_code_user_id_loan_id`:app_code, user_id, loan_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
