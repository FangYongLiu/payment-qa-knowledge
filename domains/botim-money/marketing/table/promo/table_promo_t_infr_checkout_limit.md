---
id: tbl_promo_t_infr_checkout_limit
object_type: Table
name: infr checkout limit (t_infr_checkout_limit)
aliases: [t_infr_checkout_limit, promo.t_infr_checkout_limit]
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

# infr checkout limit (t_infr_checkout_limit)

## 用途
物理表 `promo.t_infr_checkout_limit`,主键 `id`。infr checkout limit。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | varchar(32) | ulid |
| `campaign_id` | varchar(32) | merchant id |
| `owner_id` | varchar(32) | owner id |
| `kind` | varchar(10) | kind:MPC|MPCM |
| `limited` | int | limited |
| `msg` | varchar(255) | msg · 可空 |
| `off` | int | off |
| `create_at` | timestamp | created at |
| `update_at` | timestamp | updated at |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
