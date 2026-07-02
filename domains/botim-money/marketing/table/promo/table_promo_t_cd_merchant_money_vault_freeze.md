---
id: tbl_promo_t_cd_merchant_money_vault_freeze
object_type: Table
name: merchant vault freeze (t_cd_merchant_money_vault_freeze)
aliases: [t_cd_merchant_money_vault_freeze, promo.t_cd_merchant_money_vault_freeze]
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

# merchant vault freeze (t_cd_merchant_money_vault_freeze)

## 用途
物理表 `promo.t_cd_merchant_money_vault_freeze`,主键 `id`。merchant vault freeze。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | char(32) | ulid |
| `vault_id` | char(32) | vault id |
| `campaign_id` | char(32) | campaign id |
| `batch_id` | char(32) | batch id |
| `amount` | decimal(19, 4) | freeze amount of airdrop batch |
| `create_at` | timestamp | create time |
| `update_at` | timestamp | update time |

## 主键 / 索引
- 主键:`id`
- `idx_vault_batch_id`:vault_id, batch_id

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
