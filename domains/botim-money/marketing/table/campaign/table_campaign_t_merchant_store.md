---
id: tbl_campaign_t_merchant_store
object_type: Table
name: t_merchant_store (t_merchant_store)
aliases: [t_merchant_store, campaign.t_merchant_store]
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

# t_merchant_store (t_merchant_store)

## 用途
物理表 `campaign.t_merchant_store`,主键 `id`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 主键 · 可空 |
| `store_id` | bigint | 店铺id |
| `store_name` | varchar(64) | 店铺名称 · 可空 |
| `merch_id` | varchar(32) | 商户id · 可空 |
| `merch_name` | varchar(64) | 商户名称 · 可空 |
| `latitude` | double | 纬度 · 可空 |
| `longitude` | double | 经度 · 可空 |
| `location` | geometry | 地理空间 · 可空 |
| `geo_hash` | varchar(32) | 经纬度编码 · 可空 |
| `store_logo` | varchar(255) | 店铺logo · 可空 |
| `address` | varchar(255) | 店铺地址 · 可空 |
| `create_time` | timestamp | 创建时间 · 可空 |
| `update_time` | timestamp | 更新时间 · 可空 |

## 主键 / 索引
- 主键:`id`
- `uk_store_id`:store_id (UNIQUE)
- `idx_geo_hash`:geo_hash

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
