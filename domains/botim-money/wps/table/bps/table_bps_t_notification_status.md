---
id: tbl_bps_t_notification_status
object_type: Table
name: Status tracking for individual notifications (t_notification_status)
aliases: [t_notification_status, bps.t_notification_status]
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

# Status tracking for individual notifications (t_notification_status)

## 用途
物理表 `bps.t_notification_status`,主键 `notification_id, receiver_id`。Status tracking for individual notifications。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `notification_id` | char(32) | Notification unique identifier |
| `receiver_id` | varchar(32) | Receiver user ID |
| `status` | varchar(6) | Read status of the notification |
| `created_at` | timestamp | Creation time |
| `updated_at` | timestamp | Last updated time |

## 主键 / 索引
- 主键:`notification_id, receiver_id`
- 无(仅主键)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
