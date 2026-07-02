---
id: tbl_coupon_t_store
object_type: Table
name: 商户店铺 (t_store)
aliases: [t_store, coupon.t_store]
domain: marketing
status: active
owner: wujiang.ding
reviewer: wujiang.ding
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: coupon schema DDL
tags: [marketing, coupon]
sensitivity: normal
related_services: []
---

# 商户店铺 (t_store)

## 用途
物理表 `coupon.t_store`,主键 `store_id`。商户店铺。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `store_id` | bigint | 主键 |
| `store_name` | varchar(64) | 店铺名称 |
| `store_logo` | varchar(255) | 店铺图片 · 可空 |
| `mer_store_id` | bigint | 真实店铺号 · 可空 |
| `merchant_id` | bigint | 商户id |
| `merchant_name` | varchar(200) | 真实商户名称 · 可空 |
| `member_id` | varchar(32) | 真实商户id · 可空 |
| `area_id` | bigint | 区域 · 可空 |
| `address` | varchar(255) | 店铺地址 · 可空 |
| `longitude` | varchar(32) | 经度 · 可空 |
| `latitude` | varchar(32) | 纬度 · 可空 |
| `geo_code` | varchar(32) | geohash编码 · 可空 |
| `status` | varchar(12) | 状态 |
| `location` | varchar(255) | 店铺地图位置 · 可空 |
| `opening_time` | timestamp | 营业开始时间 · 可空 |
| `resting_time` | timestamp | 营业结束时间 · 可空 |
| `created_time` | timestamp | 创建时间 |
| `updated_time` | timestamp | 修改时间 |

## 主键 / 索引
- 主键:`store_id`
- `idx_created_time`:created_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
