---
id: tbl_installmentcard_t_ic_pm_payment
object_type: Table
name: Confirmed payment records linked to pay request log (t_ic_pm_payment)
aliases: [t_ic_pm_payment, installmentcard.t_ic_pm_payment]
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

# Confirmed payment records linked to pay request log (t_ic_pm_payment)

## 用途
物理表 `installmentcard.t_ic_pm_payment`,主键 `id`。Confirmed payment records linked to pay request log。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | PK · 可空 |
| `request_id` | bigint | FK to t_ic_pm_pay_request_log.id |
| `member_id` | varchar(32) | Member identifier |
| `amount` | decimal(18, 2) | Payment amount |
| `settled_amount` | decimal(18, 2) | Settled amount (populated during settlement) · 可空 |
| `pay_request_type` | tinyint | 0=MANUAL, 1=CRS |
| `created_at` | datetime(3) | Record creation time |
| `updated_at` | datetime(3) | Last update time |

## 主键 / 索引
- 主键:`id`
- `idx_member_id`:member_id
- `idx_request_id`:request_id

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
