---
id: tbl_promo_t_delivered_reward
object_type: Table
name: the reward instance which was delivered to some customer (t_delivered_reward)
aliases: [t_delivered_reward, promo.t_delivered_reward]
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

# the reward instance which was delivered to some customer (t_delivered_reward)

## 用途
物理表 `promo.t_delivered_reward`,主键 `id`。the reward instance which was delivered to some customer。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | varchar(32) | 待补 |
| `reward_id` | varchar(32) | 待补 |
| `service_id` | varchar(32) | 待补 |
| `customer_id` | varchar(32) | 待补 |
| `campaign_id` | varchar(32) | 待补 |
| `status` | varchar(20) | Status: Available, Applied, Locked, Redeemed |
| `create_at` | timestamp | 待补 |
| `update_at` | timestamp | 待补 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
