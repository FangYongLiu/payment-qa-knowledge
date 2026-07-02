---
id: tbl_installmentcard_t_ic_am_account
object_type: Table
name: Installment Card account master (t_ic_am_account)
aliases: [t_ic_am_account, installmentcard.t_ic_am_account]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: installmentcard schema DDL
tags: [lending, installmentcard]
sensitivity: normal
related_services: []
---

# Installment Card account master (t_ic_am_account)

## 用途
物理表 `installmentcard.t_ic_am_account`,主键 `id`。Installment Card account master。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | PK · 可空 |
| `member_id` | varchar(32) | Card holder member id |
| `account_no` | varchar(32) | Internal account number, unique |
| `status` | tinyint | 待补 |
| `Example` | mapping | 待补 · 可空 |
| `account_type` | tinyint | 待补 |
| `Example` | mapping | 待补 · 可空 |
| `currency` | char(3) | Account currency (ISO-4217) |
| `opened_at` | datetime(3) | Account activation/open time (Botim passes activation datetime) · 可空 |
| `closed_at` | datetime(3) | Account closure time · 可空 |
| `statement_cycle_type` | tinyint | 待补 |
| `Example` | mapping | 待补 · 可空 |
| `statement_day_of_month` | tinyint | 待补 |
| `Validate` | allowed | 待补 · 可空 |
| `repayment_day_of_month` | tinyint | 待补 |
| `Stored` | as | 待补 · 可空 |
| `limit_freeze_flag` | tinyint | Limit freeze flag as integer enum (TINYINT). PRD requires Quantix to maintain this and it must affect authorization decisions. Example mapping: 0=NO, 1=YES |
| `limit_freeze_reason` | tinyint | Optional freeze reason as integer enum (TINYINT). Example mapping (customize in code): 1=OVERDUE_INSTALLMENT, 2=OVERDUE_OTHER_PRODUCT, 3=MANUAL, 4=RISK_CONTROL · 可空 |
| `freeze_at` | datetime(3) | freeze start time for limit freeze flag/reason · 可空 |
| `freeze_end_at` | datetime(3) | freeze end time for limit freeze flag/reason · 可空 |
| `timezone` | varchar(64) | IANA timezone for statement/due date calculations |
| `version` | int | Optimistic lock version |
| `created_at` | datetime(3) | Row created time |
| `updated_at` | datetime(3) | Row updated time |

## 主键 / 索引
- 主键:`id`
- `uk_account_no`:account_no (UNIQUE)
- `idx_member_id`:member_id

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
