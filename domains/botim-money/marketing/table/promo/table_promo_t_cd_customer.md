---
id: tbl_promo_t_cd_customer
object_type: Table
name: customer (t_cd_customer)
aliases: [t_cd_customer, promo.t_cd_customer]
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

# customer (t_cd_customer)

## 用途
物理表 `promo.t_cd_customer`,主键 `id`。customer。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | char(32) | ulid |
| `owner_id` | char(32) | owner id who owns the customer |
| `uid` | varchar(64) | uid of the customer · 可空 |
| `ident` | varchar(100) | ident of the customer |
| `ident_type` | char(8) | id type enum: UniqueID, Mobile, Email |
| `ident_platform` | char(10) | the customer id source platform code: Botim |
| `payby_mid` | char(32) | payby mid · 可空 |
| `create_at` | timestamp | create time |
| `update_at` | timestamp | update time |

## 主键 / 索引
- 主键:`id`
- `idx_query_unique`:owner_id, ident_platform, ident_type, ident

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
