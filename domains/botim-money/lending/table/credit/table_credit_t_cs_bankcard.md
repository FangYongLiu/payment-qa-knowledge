---
id: tbl_credit_t_cs_bankcard
object_type: Table
name: 银行卡信息 (t_cs_bankcard)
aliases: [t_cs_bankcard, credit.t_cs_bankcard]
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

# 银行卡信息 (t_cs_bankcard)

## 用途
物理表 `credit.t_cs_bankcard`,主键 `id`。银行卡信息。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | 主键 · 可空 |
| `user_id` | varchar(50) | 用户ID |
| `account_holder_name` | varchar(200) | 用户名 |
| `iban_holder_name` | varchar(120) | iban holder name · 可空 |
| `swift_code` | varchar(50) | swift code · 可空 |
| `bank_name` | varchar(50) | bank name · 可空 |
| `type` | smallint(2) | 卡片类型 · 可空 |
| `account_num` | varchar(50) | 卡号 · 可空 |
| `account_type` | varchar(16) | account type: CURRENT/CREDIT/SAVINGS · 可空 |
| `iban` | varchar(64) | iban卡号 |
| `status` | smallint(5) | 当前状态 |
| `created_time` | timestamp | 创建时间 · 可空 |
| `last_modified` | timestamp | 修改时间 · 可空 |
| `cleaned_account_holder_name` | varchar(50) | The names of the account holders after cleaning (with removal of prefixes and special characters) · 可空 |
| `name_match_score` | decimal(4, 2) | Name matching score (0.00 - 1.00), ≥ 0.75 indicates a successful match · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_iban`:iban
- `idx_user_id`:user_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
