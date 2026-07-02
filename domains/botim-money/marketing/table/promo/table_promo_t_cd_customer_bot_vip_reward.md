---
id: tbl_promo_t_cd_customer_bot_vip_reward
object_type: Table
name: camp airdrop bot vip conf (t_cd_customer_bot_vip_reward)
aliases: [t_cd_customer_bot_vip_reward, promo.t_cd_customer_bot_vip_reward]
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

# camp airdrop bot vip conf (t_cd_customer_bot_vip_reward)

## 用途
物理表 `promo.t_cd_customer_bot_vip_reward`,主键 `id`。camp airdrop bot vip conf。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | char(32) | ulid |
| `in_campaign_id` | varchar(32) | campaign id |
| `title` | varchar(128) | title of the campaign |
| `customer_id` | varchar(32) | customer id |
| `from_merchant` | varchar(64) | merchant who gives the reward |
| `pname` | varchar(128) | product name |
| `pid` | varchar(64) | product id |
| `status` | char(8) | Status: Pending, Settled, Failed |
| `create_at` | timestamp | create time |
| `update_at` | timestamp | update time |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
