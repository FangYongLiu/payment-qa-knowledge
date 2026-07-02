---
id: tbl_promo_t_cd_camp_budget_product_conf
object_type: Table
name: budget product config (t_cd_camp_budget_product_conf)
aliases: [t_cd_camp_budget_product_conf, promo.t_cd_camp_budget_product_conf]
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

# budget product config (t_cd_camp_budget_product_conf)

## 用途
物理表 `promo.t_cd_camp_budget_product_conf`,主键 `id`。budget product config。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | char(32) | ulid |
| `merchant_id` | char(32) | merchant id |
| `campaign_id` | char(32) | campaign id |
| `product_type` | varchar(64) | product type of the campaign budget product conf |
| `product_code` | char(32) | product code of the campaign budget product conf |
| `amount` | decimal(19, 4) | amount of the campaign budget product conf |
| `vault_id` | char(32) | vault id of the merchant money vault |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
