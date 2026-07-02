---
id: tbl_household_t_hh_beneficiary
object_type: Table
name: household beneficiary (t_hh_beneficiary)
aliases: [t_hh_beneficiary, household.t_hh_beneficiary]
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

# household beneficiary (t_hh_beneficiary)

## 用途
物理表 `household.t_hh_beneficiary`,主键 `id`。household beneficiary。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | char(32) | ulid |
| `wallet_owner_id` | varchar(20) | wallet owner id |
| `group_id` | varchar(32) | group id |
| `group_type` | char(10) | group type |
| `default_type` | varchar(10) | default type: Transfer|Notify · 可空 |
| `uid` | varchar(32) | user id |
| `mobile` | varchar(20) | mobile |
| `nickname` | varchar(255) | nickname |
| `head_img_url` | varchar(256) | head image url |
| `status` | char(10) | enum:Inactive|Active|Frozen|Deleted |
| `create_at` | timestamp | create time |
| `update_at` | timestamp | update time |

## 主键 / 索引
- 主键:`id`
- `idx_wallet_owner_id`:wallet_owner_id

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
