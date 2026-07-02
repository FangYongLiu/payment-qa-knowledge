---
id: tbl_promo_t_tt_airdrop_batch
object_type: Table
name: airdrop batch (t_tt_airdrop_batch)
aliases: [t_tt_airdrop_batch, promo.t_tt_airdrop_batch]
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

# airdrop batch (t_tt_airdrop_batch)

## 用途
物理表 `promo.t_tt_airdrop_batch`,主键 `id`。airdrop batch。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | char(32) | ulid |
| `campaign_id` | char(32) | campaign id |
| `merchant_id` | char(32) | merchant id |
| `msg_app` | varchar(255) | app name of the airdrop event |
| `msg_id` | char(32) | message id of the airdrop event |
| `global_track_id` | char(32) | global track id of the airdrop event |
| `total_customer_count` | int | total customer count of the airdrop event |
| `total_amount` | decimal(19, 4) | total amount of the airdrop event |
| `successful_count` | int | successful count of the rewarded customer |
| `successful_amount` | decimal(19, 4) | successful amount of the rewarded customer |
| `pending_count` | int | pending count of the rewarded customer |
| `pending_amount` | decimal(19, 4) | pending amount of the rewarded customer |
| `status` | varchar(15) | Status: Blocked|Created|Emitted|EmittingError|Processing|Finished|Failed |
| `memo` | varchar(255) | memo of the airdrop batch failed reason · 可空 |
| `create_at` | timestamp | create time |
| `update_at` | timestamp | update time |

## 主键 / 索引
- 主键:`id`
- `idx_campaign_id`:campaign_id
- `idx_query_unique`:campaign_id, merchant_id, msg_app, msg_id
- `idx_update_at`:update_at

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
