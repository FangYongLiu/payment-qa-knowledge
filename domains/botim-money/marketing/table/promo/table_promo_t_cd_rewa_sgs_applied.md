---
id: tbl_promo_t_cd_rewa_sgs_applied
object_type: Table
name: campaign service (t_cd_rewa_sgs_applied)
aliases: [t_cd_rewa_sgs_applied, promo.t_cd_rewa_sgs_applied]
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

# campaign service (t_cd_rewa_sgs_applied)

## 用途
物理表 `promo.t_cd_rewa_sgs_applied`,主键 `id`。campaign service。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | char(32) | ulid |
| `delivered_id` | varchar(32) | campaign id |
| `ident` | varchar(32) | bot id |
| `txn_id` | varchar(32) | transaction id |
| `txn_amount` | decimal(19, 4) | transaction amount |
| `create_at` | timestamp | created at |
| `update_at` | timestamp | updated at |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
