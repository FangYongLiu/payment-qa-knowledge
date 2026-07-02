---
id: tbl_promo_t_cd_camp_bot_msg_history
object_type: Table
name: airdrop bot msg history (t_cd_camp_bot_msg_history)
aliases: [t_cd_camp_bot_msg_history, promo.t_cd_camp_bot_msg_history]
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

# airdrop bot msg history (t_cd_camp_bot_msg_history)

## 用途
物理表 `promo.t_cd_camp_bot_msg_history`,主键 `id`。airdrop bot msg history。业务语义细节**待补**(表结构来自 DDL)。

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
| `cycle_range_id` | varchar(32) | cycle range id |
| `customer_id` | varchar(64) | customer id |
| `customer_type` | varchar(15) | PromoUnique|PayByUnique|PlatformUnique |
| `source` | varchar(10) | message source from |
| `platform` | varchar(20) | enum: OS|Android|All |
| `msg` | varchar(512) | message content |
| `status` | varchar(20) | enum: Succeed|Failed|Pending|Rejected|Unknown |
| `reason` | varchar(255) | reason · 可空 |
| `create_at` | timestamp | create time |
| `update_at` | timestamp | update time |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
