---
id: tbl_promo_t_cd_rewa_applied_cashback
object_type: Table
name: applied bot vip reward (t_cd_rewa_applied_cashback)
aliases: [t_cd_rewa_applied_cashback, promo.t_cd_rewa_applied_cashback]
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

# applied bot vip reward (t_cd_rewa_applied_cashback)

## 用途
物理表 `promo.t_cd_rewa_applied_cashback`,主键 `id`。applied bot vip reward。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | char(32) | ulid |
| `amount` | decimal(19, 4) | the amount of the cashback |
| `transfer_status` | char(10) | Wait|Notified|Processing|Pending|Success|Failure |
| `create_at` | timestamp | the create time of the cashback |
| `update_at` | timestamp | the update time of the cashback |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
