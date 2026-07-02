---
id: tbl_loyalty_t_campaign_audiences
object_type: Table
name: Junction table mapping campaigns to required audiences for targeting. Populated from Talon.One campaign.attributes.audience_ids during sync. Empty = open to all users. (t_campaign_audiences)
aliases: [t_campaign_audiences, loyalty.t_campaign_audiences]
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

# Junction table mapping campaigns to required audiences for targeting. Populated from Talon.One campaign.attributes.audience_ids during sync. Empty = open to all users. (t_campaign_audiences)

## 用途
物理表 `loyalty.t_campaign_audiences`,主键 `id`。Junction table mapping campaigns to required audiences for targeting. Populated from Talon.One campaign.attributes.audience_ids during sync. Empty = open to all users.。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint unsigned | Primary key auto-increment · 可空 |
| `campaign_id` | bigint unsigned | Internal campaign ID (t_campaigns.id) |
| `audience_id` | bigint unsigned | Internal audience ID (t_audiences.id) |
| `created_at` | timestamp | Record creation timestamp |
| `updated_at` | timestamp | Record last update timestamp |

## 主键 / 索引
- 主键:`id`
- `uk_campaign_audience`:campaign_id, audience_id (UNIQUE)
- `idx_audience_id`:audience_id
- `idx_campaign_id`:campaign_id

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
