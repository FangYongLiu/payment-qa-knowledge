---
id: tbl_household_t_hh_group
object_type: Table
name: household group (t_hh_group)
aliases: [t_hh_group, household.t_hh_group]
domain: merchant-management
status: active
owner: yijian.tan
reviewer: yijian.tan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: household schema DDL
tags: [merchant-management, household]
sensitivity: normal
related_services: []
---

# household group (t_hh_group)

## 用途
物理表 `household.t_hh_group`,主键 `id`。household group。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | char(32) | ulid |
| `wallet_owner_id` | varchar(20) | wallet owner id |
| `name` | varchar(64) | group name |
| `type` | char(7) | enum:Family|Staff|Others |
| `description` | varchar(128) | description |
| `logo_url` | varchar(128) | logo url |
| `modify` | char | modify for update |
| `sort_by` | int | sort by |
| `create_at` | timestamp | create time |
| `update_at` | timestamp | update time |

## 主键 / 索引
- 主键:`id`
- `idx_wallet_owner_id`:wallet_owner_id

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
