---
id: tbl_promo_t_budget_operation_log
object_type: Table
name: budget operation log (t_budget_operation_log)
aliases: [t_budget_operation_log, promo.t_budget_operation_log]
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

# budget operation log (t_budget_operation_log)

## 用途
物理表 `promo.t_budget_operation_log`,主键 `id`。budget operation log。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | varchar(32) | ulid |
| `budget_id` | varchar(32) | budget id |
| `applied_reward_id` | varchar(32) | applied reward id |
| `campaign_id` | varchar(32) | campaign id |
| `operation_amount` | decimal(19, 4) | operation amount |
| `operation_type` | varchar(10) | operation type: DEDUCT|REFUND |
| `status` | varchar(10) | status: PENDING|SUCCESS|FAILED|REFUNDED |
| `create_at` | timestamp | created at |
| `update_at` | timestamp | updated at |

## 主键 / 索引
- 主键:`id`
- `idx_applied_reward`:applied_reward_id
- `idx_budget`:budget_id
- `idx_campaign`:campaign_id
- `idx_status`:status

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
