---
id: tbl_household_t_hh_notify_batch
object_type: Table
name: notify batch (t_hh_notify_batch)
aliases: [t_hh_notify_batch, household.t_hh_notify_batch]
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

# notify batch (t_hh_notify_batch)

## 用途
物理表 `household.t_hh_notify_batch`,主键 `id`。notify batch。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | char(32) | ulid |
| `wallet_owner_id` | varchar(20) | wallet owner id |
| `uid` | varchar(20) | uid |
| `title` | varchar(100) | title |
| `content` | varchar(128) | content · 可空 |
| `button_text` | varchar(64) | button text |
| `create_date` | timestamp | create time |
| `expired_date` | timestamp | expired time |
| `status` | char(10) | enum:Created|Pending|Success|Failed|Deleted|Expired |
| `create_at` | timestamp | create time |
| `update_at` | timestamp | update time |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
