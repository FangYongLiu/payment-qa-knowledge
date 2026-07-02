---
id: tbl_promo_t_customer
object_type: Table
name: customer (t_customer)
aliases: [t_customer, promo.t_customer]
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

# customer (t_customer)

## 用途
物理表 `promo.t_customer`,主键 `id`。customer。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | varchar(32) | 待补 |
| `owner_merchant_id` | varchar(32) | 待补 |
| `unique_identity` | varchar(100) | 待补 · 可空 |
| `identity` | varchar(100) | 待补 |
| `identity_type` | varchar(20) | id type enum: UniqueID, Mobile, Email |
| `identity_platform` | varchar(50) | the customer id source platform code: Botim |
| `origin_service_id` | varchar(32) | original service which sent the request to create this custoemr · 可空 |
| `origin_campaign_id` | varchar(32) | original campaign in which this customer participated · 可空 |
| `create_at` | timestamp | 待补 |
| `update_at` | timestamp | 待补 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
