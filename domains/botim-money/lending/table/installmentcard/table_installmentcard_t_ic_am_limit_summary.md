---
id: tbl_installmentcard_t_ic_am_limit_summary
object_type: Table
name: t_ic_am_limit_summary (t_ic_am_limit_summary)
aliases: [t_ic_am_limit_summary, installmentcard.t_ic_am_limit_summary]
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

# t_ic_am_limit_summary (t_ic_am_limit_summary)

## 用途
物理表 `installmentcard.t_ic_am_limit_summary`,主键 `id`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | Primary key · 可空 |
| `member_id` | varchar(32) | Card holder member id |
| `account_id` | bigint | Account identifier (no FK) |
| `currency` | varchar(3) | Account currency (ISO 4217, e.g. AED) |
| `credit_limit_total` | decimal(18, 2) | Approved credit limit (manual input) |
| `limit_used` | decimal(18, 2) | Captured/posted amount that consumes limit |
| `limit_pending` | decimal(18, 2) | Authorized but not captured/settled amount |
| `limit_available` | decimal(18, 2) | Available limit (stored for fast read): credit_limit_total - limit_used - limit_pending |
| `version` | int | Optimistic locking version to prevent race during concurrent auths |
| `status` | tinyint | 待补 |
| `Example` | mapping | 待补 · 可空 |
| `created_at` | datetime | Record creation timestamp |
| `updated_at` | datetime | Last record update timestamp |
| `created_by` | varchar(50) | Service or user that created the record |
| `updated_by` | varchar(50) | Service or user that last updated the record |
| `is_deleted` | tinyint | Soft delete flag: 0=false, 1=true |

## 主键 / 索引
- 主键:`id`
- `uk_account_id`:account_id (UNIQUE)
- `uk_limit_summary_member_id`:member_id (UNIQUE)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
