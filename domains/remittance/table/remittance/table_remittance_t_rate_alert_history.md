---
id: tbl_remittance_t_rate_alert_history
object_type: Table
domain: remittance
status: active
owner: lei.pan
reviewer: lei.pan
last_reviewed_at: '2026-06-25'
source_type: DB DDL
source_ref: DataGrip DDL export (remittance schema) 2026-06-25
tags:
- remittance
- remittance
- t_rate_alert_history
subdomain: remittance
module: null
sensitivity: normal
name: Table to store user-set rate alert history(t_rate_alert_history)
aliases:
- t_rate_alert_history
related_services:
- svc_remittance
related_scenarios: []
---
# Table to store user-set rate alert history(t_rate_alert_history)

## 用途
Table to store user-set rate alert history。属 remittance 库,由 [[svc_remittance]] 读写。

## 关联关系
- **所属服务**:[[svc_remittance]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / AUTO_INC | Primary key, auto-increment |
| `rate_alert_id` | bigint | NOT NULL | main table rate alert id |
| `member_id` | varchar(20) | NOT NULL | User ID |
| `base_currency` | char(3) | NOT NULL | Base currency code |
| `target_currency` | char(3) | NOT NULL | Target currency code |
| `target_country_code` | char(2) | NOT NULL | Target country code |
| `rate` | decimal(15,8) | NOT NULL | Exchange rate value |
| `notified` | tinyint | 默认 0 | Notification sent flag (0: not sent, 1: sent) |
| `last_notified` | timestamp |  | Last notification timestamp |
| `created_at` | timestamp | NOT NULL / 默认 CURRENT_TIMESTAMP | Creation timestamp |
| `updated_at` | timestamp | NOT NULL / 默认 CURRENT_TIMESTAMP | Update timestamp |
| `src` | tinyint |  | 0 AUTO, 1 MANUAL |
| `operation` | varchar(8) |  | User action to rate alert, del, create, update |
| `uid` | varchar(32) |  | uid |
| `partener_id` | varchar(20) |  | partener Id |

## 主键 / 索引
- 主键:(`id`)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
