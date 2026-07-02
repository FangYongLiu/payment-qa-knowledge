---
id: tbl_loyalty_t_vip_subscriptions_2026_12
object_type: Table
name: VIP rewards granted via loyalty campaigns - 2026-12 (t_vip_subscriptions_2026_12)
aliases: [t_vip_subscriptions_2026_12, loyalty.t_vip_subscriptions_2026_12]
domain: marketing
status: active
owner: wujiang.ding
reviewer: wujiang.ding
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: loyalty schema DDL
tags: [marketing, loyalty]
sensitivity: normal
related_services: []
---

# VIP rewards granted via loyalty campaigns - 2026-12 (t_vip_subscriptions_2026_12)

## 用途
物理表 `loyalty.t_vip_subscriptions_2026_12`,主键 `id`。VIP rewards granted via loyalty campaigns - 2026-12。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint unsigned | Primary key auto-increment · 可空 |
| `user_id` | bigint unsigned | FK to t_users.id |
| `ucid` | varchar(50) | User UCID (uppercase) for VIP API |
| `campaign_id` | bigint unsigned | FK to t_campaigns.id - Campaign that granted VIP · 可空 |
| `achievement_id` | bigint unsigned | FK to t_achievements.id · 可空 |
| `source_event_id` | varchar(100) | Event that triggered VIP grant |
| `pid` | varchar(100) | VIP product ID for Botim API |
| `pname` | varchar(200) | VIP product name for display · 可空 |
| `status` | varchar(10) | Status: pending|active|failed |
| `vip_request_id` | varchar(100) | Idempotency key (VIP{t_custom_effects.id}) - set when API called · 可空 |
| `failure_reason` | varchar(100) | 待补 · 可空 |
| `failure_code` | varchar(50) | 待补 · 可空 |
| `granted_at` | timestamp | When VIP API returned success · 可空 |
| `created_at` | timestamp | Record creation timestamp |
| `updated_at` | timestamp | Record last update timestamp |

## 主键 / 索引
- 主键:`id`
- `uk_vip_request_id`:vip_request_id (UNIQUE)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
