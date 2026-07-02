---
id: tbl_rnpl_t_user_quota
object_type: Table
name: User Credit Limit Table (t_user_quota)
aliases: [t_user_quota, rnpl.t_user_quota]
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

# User Credit Limit Table (t_user_quota)

## 用途
物理表 `rnpl.t_user_quota`,主键 `id`。User Credit Limit Table。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | 待补 · 可空 |
| `user_id` | varchar(20) | user id |
| `business_code` | varchar(20) | business code |
| `total_amount` | decimal(15, 2) | credit limit |
| `currency` | char(3) | currency |
| `status` | smallint(4) | Status: 1 Normal, -1 Invalid |
| `expire_time` | timestamp | expiry (expiration) time · 可空 |
| `create_time` | timestamp | storage time |
| `update_time` | datetime | last update time |
| `use_conditions` | varchar(255) | conditions for use of the line association: Rnpl association conditions include: total_profit_rate: use this line rate; include_deposit: 0 is not included, 1 is included; include_broker_fee: 0 is not included, 1 is included · 可空 |
| `bus_record_id` | int | the business event id that brought in this amount, currently associated with the id of the t_credit_order table record · 可空 |

## 主键 / 索引
- 主键:`id`
- `uk_uid`:user_id, business_code (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
