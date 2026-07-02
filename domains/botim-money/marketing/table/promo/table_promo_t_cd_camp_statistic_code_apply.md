---
id: tbl_promo_t_cd_camp_statistic_code_apply
object_type: Table
name: statistic code apply (t_cd_camp_statistic_code_apply)
aliases: [t_cd_camp_statistic_code_apply, promo.t_cd_camp_statistic_code_apply]
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

# statistic code apply (t_cd_camp_statistic_code_apply)

## 用途
物理表 `promo.t_cd_camp_statistic_code_apply`,主键 `id`。statistic code apply。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | char(32) | ulid |
| `merchant_id` | varchar(32) | merchant id |
| `campaign_id` | varchar(32) | campaign id |
| `code_id` | varchar(32) | promo code id |
| `title` | varchar(100) | title |
| `description` | varchar(255) | description · 可空 |
| `customer_id` | varchar(32) | customer id · 可空 |
| `customer_type` | varchar(30) | customer type · 可空 |
| `code` | varchar(20) | statistic code |
| `create_at` | timestamp | created at |
| `update_at` | timestamp | updated at |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
