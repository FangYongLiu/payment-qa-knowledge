---
id: tbl_promo_t_cd_rewa_conf_discount_calc_rule
object_type: Table
name: extra reward conf for discount calculate rules (t_cd_rewa_conf_discount_calc_rule)
aliases: [t_cd_rewa_conf_discount_calc_rule, promo.t_cd_rewa_conf_discount_calc_rule]
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

# extra reward conf for discount calculate rules (t_cd_rewa_conf_discount_calc_rule)

## 用途
物理表 `promo.t_cd_rewa_conf_discount_calc_rule`,主键 `id`。extra reward conf for discount calculate rules。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | char(32) | ulid |
| `conf_id` | varchar(32) | reward conf id |
| `campaign_id` | varchar(32) | campaign id |
| `name` | varchar(20) | the name of the rule |
| `json` | varchar(1024) | the apply rules in JSON |
| `create_at` | timestamp | the create time of the discount calc rule |
| `update_at` | timestamp | the update time of the discount calc rule |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
