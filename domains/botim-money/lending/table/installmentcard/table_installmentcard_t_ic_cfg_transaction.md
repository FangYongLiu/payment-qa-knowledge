---
id: tbl_installmentcard_t_ic_cfg_transaction
object_type: Table
name: Transaction processing configuration (authorization limits) (t_ic_cfg_transaction)
aliases: [t_ic_cfg_transaction, installmentcard.t_ic_cfg_transaction]
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

# Transaction processing configuration (authorization limits) (t_ic_cfg_transaction)

## 用途
物理表 `installmentcard.t_ic_cfg_transaction`,主键 `id`。Transaction processing configuration (authorization limits)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | Primary key · 可空 |
| `config_code` | varchar(32) | Config code for future multi-config support |
| `currency` | varchar(3) | Currency |
| `min_txn_amount` | decimal(18, 2) | Minimum transaction amount |
| `max_txn_amount` | decimal(18, 2) | Maximum single transaction amount |
| `daily_txn_limit` | decimal(18, 2) | Maximum daily transaction total · 可空 |
| `daily_txn_count` | int | Maximum daily transaction count · 可空 |
| `monthly_txn_limit` | decimal(18, 2) | Maximum monthly transaction total · 可空 |
| `status` | tinyint | 0=INACTIVE, 1=ACTIVE |
| `effective_from` | date | Effective start date |
| `effective_to` | date | Effective end date (NULL = no expiry) · 可空 |
| `created_at` | datetime(3) | 待补 |
| `updated_at` | datetime(3) | 待补 |

## 主键 / 索引
- 主键:`id`
- `uk_config_code`:config_code (UNIQUE)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
