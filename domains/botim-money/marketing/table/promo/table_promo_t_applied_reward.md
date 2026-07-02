---
id: tbl_promo_t_applied_reward
object_type: Table
name: applied reward (t_applied_reward)
aliases: [t_applied_reward, promo.t_applied_reward]
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

# applied reward (t_applied_reward)

## 用途
物理表 `promo.t_applied_reward`,主键 `id`。applied reward。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | varchar(32) | 待补 |
| `delivered_reward_id` | varchar(32) | 待补 |
| `transaction_id` | varchar(32) | 待补 |
| `transaction_amount` | decimal(10, 4) | 待补 |
| `rewarded_amount` | decimal(10, 4) | 待补 |
| `merchant_id` | varchar(32) | 待补 |
| `service_id` | varchar(32) | 待补 |
| `campaign_id` | varchar(32) | 待补 |
| `merchant_fund_id` | varchar(32) | 待补 |
| `merchant_fund_channel` | varchar(50) | 待补 |
| `merchant_fund_account` | varchar(50) | 待补 |
| `hit_rule` | varchar(255) | 待补 |
| `status` | varchar(20) | Status: Applied, Locked, Redeemed, Refunded, Abandoned |
| `create_at` | timestamp | 待补 |
| `update_at` | timestamp | 待补 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
