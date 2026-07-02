---
id: tbl_promo_t_budget_control
object_type: Table
name: budget control (t_budget_control)
aliases: [t_budget_control, promo.t_budget_control]
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

# budget control (t_budget_control)

## 用途
物理表 `promo.t_budget_control`,主键 `id`。budget control。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | varchar(32) | ulid |
| `campaign_id` | varchar(32) | campaign id |
| `merchant_id` | varchar(32) | merchant id |
| `total_amount` | decimal(19, 4) | total amount |
| `used_amount` | decimal(19, 4) | used amount |
| `currency` | char(3) | currency |
| `version` | int | version |
| `status` | varchar(10) | status: ACTIVE|INACTIVE |
| `create_at` | timestamp | create at |
| `update_at` | timestamp | update at |

## 主键 / 索引
- 主键:`id`
- `idx_campaign`:campaign_id
- `idx_merchant`:merchant_id

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
