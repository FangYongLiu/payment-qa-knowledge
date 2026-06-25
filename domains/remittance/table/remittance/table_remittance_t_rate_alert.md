---
id: tbl_remittance_t_rate_alert
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
- t_rate_alert
subdomain: remittance
module: null
sensitivity: normal
name: Table to store user-set rate alert(t_rate_alert)
aliases:
- t_rate_alert
related_services:
- svc_remittance
related_scenarios: []
---
# Table to store user-set rate alert(t_rate_alert)

## 用途
Table to store user-set rate alert。属 remittance 库,由 [[svc_remittance]] 读写。

## 关联关系
- **所属服务**:[[svc_remittance]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / AUTO_INC | Primary key, auto-increment |
| `member_id` | varchar(20) | NOT NULL | User ID |
| `base_currency` | char(3) | NOT NULL | Base currency code |
| `target_currency` | char(3) | NOT NULL | Target currency code |
| `target_country_code` | char(2) | NOT NULL | Target country code |
| `rate` | decimal(15,8) | NOT NULL | Exchange rate value |
| `notified` | tinyint | 默认 0 | Notification sent flag (0: not sent, 1: sent) |
| `last_notified` | timestamp |  | Last notification timestamp |
| `created_at` | timestamp | NOT NULL / 默认 CURRENT_TIMESTAMP | Creation timestamp |
| `updated_at` | timestamp | NOT NULL / 默认 CURRENT_TIMESTAMP | Update timestamp |
| `src` | tinyint |  | AUTO,MANUAL |
| `uid` | varchar(32) |  | uid |
| `partener_id` | varchar(20) |  | partener Id |

## 主键 / 索引
- 主键:(`id`)
- 唯一约束:
  - `uk_rate_alert_mbtt` 唯一 (member_id, base_currency, target_currency, target_country_code)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
