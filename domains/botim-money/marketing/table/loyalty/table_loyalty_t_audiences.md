---
id: tbl_loyalty_t_audiences
object_type: Table
name: Talon.One audience definitions for campaign targeting (t_audiences)
aliases: [t_audiences, loyalty.t_audiences]
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

# Talon.One audience definitions for campaign targeting (t_audiences)

## 用途
物理表 `loyalty.t_audiences`,主键 `id`。Talon.One audience definitions for campaign targeting。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint unsigned | Primary key auto-increment · 可空 |
| `talon_audience_id` | int | Audience ID in Talon.One |
| `name` | varchar(100) | Audience name |
| `description` | varchar(150) | Audience description · 可空 |
| `source` | varchar(10) | Audience source system: talon|moengage|csv|api |
| `source_cohort_id` | varchar(100) | External cohort ID (e.g., MoEngage cohort ID) · 可空 |
| `member_count` | int unsigned | Approximate member count |
| `shard_index` | tinyint unsigned | Shard table index (1-5) for audience members storage · 可空 |
| `is_active` | tinyint(1) | Whether audience is active |
| `synced_at` | timestamp | Last sync timestamp · 可空 |
| `warmed_at` | timestamp | When audience cache was last successfully warmed · 可空 |
| `created_at` | timestamp | Record creation timestamp |
| `updated_at` | timestamp | Record last update timestamp |

## 主键 / 索引
- 主键:`id`
- `uk_audiences_name`:name (UNIQUE)
- `uk_audiences_talon_id`:talon_audience_id (UNIQUE)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
