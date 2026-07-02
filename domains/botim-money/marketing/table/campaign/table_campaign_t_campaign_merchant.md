---
id: tbl_campaign_t_campaign_merchant
object_type: Table
name: t_campaign_merchant (t_campaign_merchant)
aliases: [t_campaign_merchant, campaign.t_campaign_merchant]
domain: marketing
status: active
owner: wujiang.ding
reviewer: wujiang.ding
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: campaign schema DDL
tags: [marketing, campaign]
sensitivity: normal
related_services: []
---

# t_campaign_merchant (t_campaign_merchant)

## 用途
物理表 `campaign.t_campaign_merchant`,主键 `id`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 主键 · 可空 |
| `merch_id` | varchar(32) | 商户id · 可空 |
| `merch_name` | varchar(50) | 商户名称 · 可空 |
| `merch_logo` | varchar(125) | 商户logo · 可空 |
| `cmpn_id` | bigint | 活动id · 可空 |
| `create_time` | timestamp | 创建时间 · 可空 |
| `update_time` | timestamp | 更新时间 · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_cmpn_id`:cmpn_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
