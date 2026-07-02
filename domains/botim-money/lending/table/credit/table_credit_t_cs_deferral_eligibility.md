---
id: tbl_credit_t_cs_deferral_eligibility
object_type: Table
name: Deferral eligibility records from Collection System (t_cs_deferral_eligibility)
aliases: [t_cs_deferral_eligibility, credit.t_cs_deferral_eligibility]
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

# Deferral eligibility records from Collection System (t_cs_deferral_eligibility)

## 用途
物理表 `credit.t_cs_deferral_eligibility`,主键 `id`。Deferral eligibility records from Collection System。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | Primary key · 可空 |
| `user_id` | varchar(20) | CashNow user identifier |
| `deferral_id` | varchar(64) | Unique id from Collection System |
| `order_no` | varchar(64) | Target order no |
| `bill_id` | int | Target bill id |
| `coupon_id` | varchar(64) | Coupon id if coupon is available · 可空 |
| `status` | tinyint | 1.pending 2.accepted 3.expired |
| `accepted_at` | datetime | Timestamp when user accepts deferral · 可空 |
| `offer_expired_at` | datetime | Offer expiry time · 可空 |
| `created_time` | datetime | Record creation timestamp |
| `last_modified` | datetime | Last update timestamp |

## 主键 / 索引
- 主键:`id`
- `uk_deferral_id`:deferral_id (UNIQUE)
- `idx_user_order`:user_id, order_no

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
