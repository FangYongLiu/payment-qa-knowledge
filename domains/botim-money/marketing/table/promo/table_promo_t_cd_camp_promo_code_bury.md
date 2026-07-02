---
id: tbl_promo_t_cd_camp_promo_code_bury
object_type: Table
name: promo code bury (t_cd_camp_promo_code_bury)
aliases: [t_cd_camp_promo_code_bury, promo.t_cd_camp_promo_code_bury]
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

# promo code bury (t_cd_camp_promo_code_bury)

## 用途
物理表 `promo.t_cd_camp_promo_code_bury`,主键 `id`。promo code bury。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | char(32) | ulid |
| `campaign_id` | char(32) | campaign id |
| `owner_id` | char(32) | owner id |
| `bury` | varchar(2024) | json:bury data json string |
| `create_at` | timestamp | create time |
| `update_at` | timestamp | update time |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
