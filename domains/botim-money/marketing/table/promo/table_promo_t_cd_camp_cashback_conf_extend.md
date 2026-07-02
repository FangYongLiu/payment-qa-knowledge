---
id: tbl_promo_t_cd_camp_cashback_conf_extend
object_type: Table
name: airdrop cashback preset amount (t_cd_camp_cashback_conf_extend)
aliases: [t_cd_camp_cashback_conf_extend, promo.t_cd_camp_cashback_conf_extend]
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

# airdrop cashback preset amount (t_cd_camp_cashback_conf_extend)

## 用途
物理表 `promo.t_cd_camp_cashback_conf_extend`,主键 `id`。airdrop cashback preset amount。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | char(32) | ulid |
| `merchant_id` | varchar(32) | applied reward id |
| `campaign_id` | varchar(32) | campaign id |
| `preset_amount` | decimal(19, 4) | preset amount |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
