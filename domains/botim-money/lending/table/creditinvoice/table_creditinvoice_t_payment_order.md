---
id: tbl_creditinvoice_t_payment_order
object_type: Table
name: t_payment_order (t_payment_order)
aliases: [t_payment_order, creditinvoice.t_payment_order]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: creditinvoice schema DDL
tags: [lending, creditinvoice]
sensitivity: normal
related_services: []
---

# t_payment_order (t_payment_order)

## 用途
物理表 `creditinvoice.t_payment_order`,主键 `id`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint unsigned | 待补 · 可空 |
| `payment_no` | varchar(64) | PAY-YYYYMMDDHHmmss-{6 digits} |
| `member_id` | varchar(20) | member id |
| `eid` | varchar(64) | 待补 · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_biz_ref_no`:biz_ref_no
- `idx_eid`:eid
- `idx_eid_hash`:eid_hash
- `idx_member_id`:member_id
- `idx_status_notify`:payment_status, last_notify_time
- `idx_status_paid_time`:payment_status, paid_time

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
