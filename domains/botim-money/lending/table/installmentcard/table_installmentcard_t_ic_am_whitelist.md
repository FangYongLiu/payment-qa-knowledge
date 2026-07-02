---
id: tbl_installmentcard_t_ic_am_whitelist
object_type: Table
name: t_ic_am_whitelist (t_ic_am_whitelist)
aliases: [t_ic_am_whitelist, installmentcard.t_ic_am_whitelist]
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

# t_ic_am_whitelist (t_ic_am_whitelist)

## 用途
物理表 `installmentcard.t_ic_am_whitelist`,主键 `id`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | Primary key · 可空 |
| `member_id` | varchar(32) | External member/customer identifier (no FK) |
| `account_id` | bigint | Account identifier (nullable if whitelist created before account creation) · 可空 |
| `credit_limit` | decimal(18, 2) | Approved credit limit |
| `whitelist_status` | tinyint | 待补 |
| `Example` | mapping | 待补 · 可空 |
| `reason` | varchar(255) | Reason for whitelist approval or revocation · 可空 |
| `effective_from` | datetime | Whitelist effective start time · 可空 |
| `effective_to` | datetime | Whitelist effective end time (NULL means no expiry) · 可空 |
| `created_at` | datetime | Record creation timestamp · 可空 |
| `updated_at` | datetime | Last record update timestamp · 可空 |
| `created_by` | varchar(50) | Service or user that created the record |
| `updated_by` | varchar(50) | Service or user that last updated the record |
| `is_deleted` | tinyint | Soft delete flag: 0=false, 1=true |
| `cached_at` | timestamp | NULL = dirty; needs to be reflected in the Redis whitelist cache. Non-NULL = caught up at this time. · 可空 |

## 主键 / 索引
- 主键:`id`
- `uk_member_account`:member_id, account_id (UNIQUE)
- `idx_account_id`:account_id
- `idx_cached_at`:cached_at

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
