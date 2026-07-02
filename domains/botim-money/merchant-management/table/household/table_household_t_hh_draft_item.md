---
id: tbl_household_t_hh_draft_item
object_type: Table
name: household item (t_hh_draft_item)
aliases: [t_hh_draft_item, household.t_hh_draft_item]
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

# household item (t_hh_draft_item)

## 用途
物理表 `household.t_hh_draft_item`,主键 `id`。household item。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | char(32) | ulid |
| `wallet_owner_id` | varchar(20) | wallet owner id |
| `beneficiary_id` | varchar(32) | beneficiary id |
| `group_id` | varchar(32) | group id |
| `group_type` | char(7) | group type: Family|Staff|Others |
| `type` | char(8) | enum:Transfer|Notify |
| `item_id` | varchar(32) | item id |
| `status` | varchar(8) | enum:Inactive|Active |
| `create_at` | timestamp | create time |
| `update_at` | timestamp | update time |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
