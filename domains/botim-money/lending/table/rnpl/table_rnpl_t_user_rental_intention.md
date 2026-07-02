---
id: tbl_rnpl_t_user_rental_intention
object_type: Table
name: User Rental Intention Information Table (t_user_rental_intention)
aliases: [t_user_rental_intention, rnpl.t_user_rental_intention]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: rnpl schema DDL
tags: [lending, rnpl]
sensitivity: normal
related_services: []
---

# User Rental Intention Information Table (t_user_rental_intention)

## 用途
物理表 `rnpl.t_user_rental_intention`,主键 `id`。User Rental Intention Information Table。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | 待补 · 可空 |
| `user_id` | varchar(20) | user id |
| `email_address` | varchar(64) | email · 可空 |
| `property_type` | varchar(20) | property type · 可空 |
| `emirate` | varchar(20) | emirate · 可空 |
| `area` | varchar(32) | area · 可空 |
| `has_identified_property` | smallint | has identified property · 可空 |
| `user_budget_estimate` | decimal(10, 2) | User provided annual rental budget · 可空 |
| `is_moving_in_next_two_month` | tinyint | Indicates if the user is planning to move/renew in the next two months · 可空 |
| `user_move_in_date_estimate` | timestamp | User-provided planned move/renewal date · 可空 |
| `user_self_reported_salary` | decimal(10, 2) | User-provided monthly salary in AED · 可空 |
| `create_time` | timestamp | 待补 |
| `update_time` | timestamp | 待补 |

## 主键 / 索引
- 主键:`id`
- `uk_uid`:user_id (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
