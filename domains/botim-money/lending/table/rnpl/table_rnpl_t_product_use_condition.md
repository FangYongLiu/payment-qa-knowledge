---
id: tbl_rnpl_t_product_use_condition
object_type: Table
name: t_product_use_condition (t_product_use_condition)
aliases: [t_product_use_condition, rnpl.t_product_use_condition]
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

# t_product_use_condition (t_product_use_condition)

## 用途
物理表 `rnpl.t_product_use_condition`,主键 `id`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | Primary key, auto-increment · 可空 |
| `profile_id` | int | Profile ID associated with the user · 可空 |
| `user_id` | varchar(32) | BOTIM User ID |
| `email` | varchar(100) | Email address of the user · 可空 |
| `mobile` | varchar(20) | Mobile number of the user · 可空 |
| `user_condition_status` | tinyint | Condition status: 1- ACTIVE, 0- INACTIVE · 可空 |
| `use_condition` | varchar(255) | A JSON object in key-value pair format · 可空 |
| `created_time` | timestamp | Record creation timestamp · 可空 |
| `update_time` | timestamp | Record update timestamp · 可空 |

## 主键 / 索引
- 主键:`id`
- `uk_t_product_use_condition_email`:email (UNIQUE)
- `uk_t_product_use_condition_mobile`:mobile (UNIQUE)
- `user_id`:user_id (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
