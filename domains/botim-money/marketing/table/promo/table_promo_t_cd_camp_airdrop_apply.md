---
id: tbl_promo_t_cd_camp_airdrop_apply
object_type: Table
name: airdrop apply record (t_cd_camp_airdrop_apply)
aliases: [t_cd_camp_airdrop_apply, promo.t_cd_camp_airdrop_apply]
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

# airdrop apply record (t_cd_camp_airdrop_apply)

## 用途
物理表 `promo.t_cd_camp_airdrop_apply`,主键 `id`。airdrop apply record。业务语义细节**待补**(表结构来自 DDL)。

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
| `customer_id` | varchar(64) | customer id |
| `customer_kind` | varchar(15) | PromoUnique|PayByUnique|PlatformUnique |
| `kind` | varchar(20) | event type |
| `preset_amount` | decimal(19, 4) | airdrop preset amount · 可空 |
| `create_at` | timestamp | create time |
| `update_at` | timestamp | update time |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
