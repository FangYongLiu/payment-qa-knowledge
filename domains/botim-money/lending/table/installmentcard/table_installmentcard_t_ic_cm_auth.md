---
id: tbl_installmentcard_t_ic_cm_auth
object_type: Table
name: Authorization holds for limit reservation (t_ic_cm_auth)
aliases: [t_ic_cm_auth, installmentcard.t_ic_cm_auth]
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

# Authorization holds for limit reservation (t_ic_cm_auth)

## 用途
物理表 `installmentcard.t_ic_cm_auth`,主键 `id`。Authorization holds for limit reservation。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | Primary key (internal authorization/hold identifier) · 可空 |
| `member_id` | varchar(32) | External member/customer identifier (string, no FK dependency) |
| `txn_id` | bigint | Logical reference to t_ic_cm_card_txn.id (no FK constraint) |
| `account_id` | bigint | Logical reference to t_ic_am_account.id (no FK constraint) |
| `auth_code` | varchar(50) | Authorization code from PPC/gateway (nullable if declined/absent) · 可空 |
| `auth_amount` | decimal(18, 2) | Authorized/held amount for this auth event |
| `captured_amount` | decimal(18, 2) | Amount captured against this auth (supports partial capture) |
| `released_amount` | decimal(18, 2) | Amount released back to available limit |
| `currency` | varchar(3) | Currency code (ISO 4217), e.g., AED |
| `auth_status` | tinyint | Authorization status: 0=HELD, 1=RELEASED, 2=CAPTURED, 3=PARTIALLY_CAPTURED, 4=EXPIRED, 5=DECLINED |
| `hold_expires_at` | datetime | When the hold expires (PRD: up to 3 months) · 可空 |
| `idempotency_key` | varchar(100) | Unique idempotency key from PPC/gateway for this auth event |
| `created_at` | datetime | Record creation time |
| `updated_at` | datetime | Record last update time |
| `created_by` | varchar(50) | Service/user that created the record |
| `updated_by` | varchar(50) | Service/user that last updated the record |
| `is_deleted` | tinyint | Soft delete flag: 0=false, 1=true |

## 主键 / 索引
- 主键:`id`
- `uk_idempotency_key`:idempotency_key (UNIQUE)
- `idx_account_status`:account_id, auth_status
- `idx_member_id`:member_id
- `idx_txn_id`:txn_id

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
