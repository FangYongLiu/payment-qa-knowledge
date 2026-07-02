---
id: tbl_promo_t_cd_rewa_refund_discount_record
object_type: Table
name: refund reward discount record (t_cd_rewa_refund_discount_record)
aliases: [t_cd_rewa_refund_discount_record, promo.t_cd_rewa_refund_discount_record]
domain: marketing
status: active
owner: wujiang.ding
reviewer: wujiang.ding
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: promo schema DDL
tags: [marketing, promo]
sensitivity: normal
related_services: []
---

# refund reward discount record (t_cd_rewa_refund_discount_record)

## 用途
物理表 `promo.t_cd_rewa_refund_discount_record`,主键 `id`。refund reward discount record。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | char(32) | ulid |
| `campaign_id` | varchar(32) | campaign id |
| `applied_reward_id` | varchar(32) | reward conf id |
| `txn_id` | varchar(64) | transactin id |
| `refund_id` | varchar(64) | refund id |
| `refund_amount` | decimal(19, 4) | refund amount |
| `status` | char(8) | enums: Refunded|Locked|Unlock |
| `create_at` | timestamp | create time |
| `update_at` | timestamp | update time |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
