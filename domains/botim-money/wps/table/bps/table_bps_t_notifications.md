---
id: tbl_bps_t_notifications
object_type: Table
name: Notifications table for corporate users (t_notifications)
aliases: [t_notifications, bps.t_notifications]
domain: wps
status: active
owner: xinwei.cao
reviewer: xinwei.cao
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: bps schema DDL
tags: [wps, bps]
sensitivity: normal
related_services: []
---

# Notifications table for corporate users (t_notifications)

## 用途
物理表 `bps.t_notifications`,主键 `id`。Notifications table for corporate users。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | char(32) | Primary key |
| `corporate_id` | varchar(32) | Corporate identifier |
| `creater_id` | varchar(32) | Creator identifier |
| `creater_name` | varchar(32) | Creator name |
| `merchant_mid` | varchar(32) | Merchant identifier |
| `type` | varchar(32) | Notification type |
| `user_role` | varchar(32) | User role who created this notification |
| `message` | varchar(512) | Notification message |
| `metadata` | varchar(512) | Additional metadata in JSON format · 可空 |
| `created_at` | timestamp | Creation time |
| `updated_at` | timestamp | Last updated time |

## 主键 / 索引
- 主键:`id`
- `idx_corporate_created`:corporate_id, created_at

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
