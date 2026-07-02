---
id: tbl_remittance_t_remittance_alert
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
- t_remittance_alert
subdomain: remittance
module: null
sensitivity: normal
name: remittance alert table(t_remittance_alert)
aliases:
- t_remittance_alert
related_services:
- svc_remittance
related_scenarios: []
---
# remittance alert table(t_remittance_alert)

## 用途
remittance alert table。属 remittance 库,由 [[svc_remittance]] 读写。

## 关联关系
- **所属服务**:[[svc_remittance]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | int | PK / AUTO_INC | id |
| `alert_key` | varchar(50) |  | alert key |
| `alert_date` | varchar(10) |  | alert date:20240901 |
| `alert_info` | varchar(150) |  | alert info |
| `alert_type` | varchar(32) |  | alert type（MG_CODETABLE：MG） |
| `channel_code` | varchar(32) |  | channel code |
| `status` | varchar(16) | NOT NULL | alert status：NORMAL,ERROR |
| `create_time` | timestamp |  | create time |
| `update_time` | timestamp |  | update time |
| `extension` | varchar(1000) |  | ext |

## 主键 / 索引
- 主键:(`id`)
- 唯一约束:
  - `t_remittance_alert_uk` 唯一 (alert_key, alert_date)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
