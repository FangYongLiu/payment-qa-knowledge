---
id: tbl_remittance_t_success_rate_log
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
- t_success_rate_log
subdomain: remittance
module: null
sensitivity: normal
name: Table to save corridor success rate(t_success_rate_log)
aliases:
- t_success_rate_log
related_services:
- svc_remittance
related_scenarios: []
---
# Table to save corridor success rate(t_success_rate_log)

## 用途
Table to save corridor success rate。属 remittance 库,由 [[svc_remittance]] 读写。

## 关联关系
- **所属服务**:[[svc_remittance]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / AUTO_INC | Primary key, auto-increment |
| `channel_code` | varchar(20) | NOT NULL | Channel code |
| `config_json` | varchar(255) |  | channel config json |
| `success_rate` | decimal(10,2) |  | Success rate |
| `max_score` | bigint |  | Latest max score of set |
| `created_at` | timestamp | NOT NULL / 默认 CURRENT_TIMESTAMP | Creation timestamp |
| `updated_at` | timestamp | NOT NULL / 默认 CURRENT_TIMESTAMP | Update timestamp |

## 主键 / 索引
- 主键:(`id`)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
