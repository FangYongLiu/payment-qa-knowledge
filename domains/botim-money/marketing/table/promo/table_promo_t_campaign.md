---
id: tbl_promo_t_campaign
object_type: Table
name: marketing campaign (t_campaign)
aliases: [t_campaign, promo.t_campaign]
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

# marketing campaign (t_campaign)

## 用途
物理表 `promo.t_campaign`,主键 `id`。marketing campaign。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | varchar(32) | 待补 |
| `campaign_code` | varbinary(60) | 待补 |
| `merchant_id` | varchar(32) | 待补 |
| `scope_type` | varchar(20) | the scope type enum: General, ApplyToServices |
| `short_name` | varchar(60) | 待补 |
| `long_name` | varchar(120) | 待补 |
| `description` | varchar(600) | 待补 |
| `landing_page` | varchar(500) | 待补 |
| `start_at` | timestamp | 待补 |
| `end_at` | timestamp | 待补 |
| `max_participants` | bigint | if the value is 0, then no constraints for the participants quantity |
| `status` | varchar(20) | Campaign Status: Preparing, Running, Paused, Terminated, Ended |
| `sort` | int | 待补 |
| `create_at` | timestamp | 待补 |
| `update_at` | timestamp | 待补 |

## 主键 / 索引
- 主键:`id`
- `u_code`:campaign_code (UNIQUE)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
