---
id: tbl_promo_t_tt_airdrop_task
object_type: Table
name: airdrop task (t_tt_airdrop_task)
aliases: [t_tt_airdrop_task, promo.t_tt_airdrop_task]
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

# airdrop task (t_tt_airdrop_task)

## 用途
物理表 `promo.t_tt_airdrop_task`,主键 `id`。airdrop task。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | char(32) | ulid |
| `batch_id` | char(32) | batch id |
| `customer_id` | char(32) | customer id |
| `amount` | decimal(19, 4) | amount of the customer reward |
| `merchant_id` | char(32) | merchant id |
| `campaign_id` | char(32) | campaign id |
| `vault_id` | char(32) | vault id |
| `status` | varchar(15) | Status: Created|Executing|Success|Failed |
| `payment_status` | varchar(15) | Status: Init |
| `create_at` | timestamp | create time |
| `update_at` | timestamp | update time |

## 主键 / 索引
- 主键:`id`
- `idx_batch_status`:batch_id, status
- `idx_task_query`:campaign_id, customer_id, merchant_id

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
