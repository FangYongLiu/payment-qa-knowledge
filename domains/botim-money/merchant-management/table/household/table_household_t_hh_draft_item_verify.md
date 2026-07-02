---
id: tbl_household_t_hh_draft_item_verify
object_type: Table
name: household item (t_hh_draft_item_verify)
aliases: [t_hh_draft_item_verify, household.t_hh_draft_item_verify]
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

# household item (t_hh_draft_item_verify)

## 用途
物理表 `household.t_hh_draft_item_verify`,主键 `id`。household item。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | char(32) | ulid |
| `draft_id` | varchar(32) | draft id |
| `kind` | char(8) | enum:Contract|Identity |
| `next_step_id` | varchar(32) | next step id |
| `create_at` | timestamp | create time |
| `update_at` | timestamp | update time |

## 主键 / 索引
- 主键:`id`
- `idx_pay_draft_id`:draft_id

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
