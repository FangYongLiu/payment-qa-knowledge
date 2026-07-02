---
id: tbl_remittance_t_corridor_fail_log
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
- t_corridor_fail_log
subdomain: remittance
module: null
sensitivity: normal
name: Log table for remittance channel failure details(t_corridor_fail_log)
aliases:
- t_corridor_fail_log
related_services:
- svc_remittance
related_scenarios: []
---
# Log table for remittance channel failure details(t_corridor_fail_log)

## 用途
Log table for remittance channel failure details。属 remittance 库,由 [[svc_remittance]] 读写。

## 关联关系
- **所属服务**:[[svc_remittance]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | int(20) | PK / AUTO_INC | Primary key |
| `order_no` | varchar(32) |  | Remittance order code |
| `fail_from` | varchar(12) | NOT NULL | Source of failure |
| `channel_code` | varchar(12) | NOT NULL | Channel code |
| `response_code` | varchar(32) | NOT NULL | Channel error response status code |
| `response_sub_code` | varchar(32) |  | Channel error response sub-status code |
| `response_msg` | varchar(500) |  | Failure reason returned by the channel |
| `i18n_key` | varchar(50) |  | Internationalization key for user-visible message |
| `create_time` | timestamp | NOT NULL | Creation time |
| `update_time` | timestamp | NOT NULL | Modification time |

## 主键 / 索引
- 主键:(`id`)
- 唯一约束:
  - `corridor_fail_log_order_no_IDX` 唯一 (order_no, fail_from)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
