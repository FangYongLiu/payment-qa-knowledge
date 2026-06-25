---
id: tbl_remittance_t_corridor_fail_show_config
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
- t_corridor_fail_show_config
subdomain: remittance
module: null
sensitivity: normal
name: Client display configuration table for channel error codes(t_corridor_fail_show_config)
aliases:
- t_corridor_fail_show_config
related_services:
- svc_remittance
related_scenarios: []
---
# Client display configuration table for channel error codes(t_corridor_fail_show_config)

## 用途
Client display configuration table for channel error codes。属 remittance 库,由 [[svc_remittance]] 读写。

## 关联关系
- **所属服务**:[[svc_remittance]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | int(10) | PK / AUTO_INC | Primary key |
| `channel_code` | varchar(12) | NOT NULL | Channel code |
| `response_code` | varchar(8) | NOT NULL | Channel error response status code |
| `response_sub_code` | varchar(8) |  | Channel error response sub-status code |
| `i18n_key` | varchar(50) | NOT NULL | Internationalization key for user-visible message |
| `create_time` | timestamp | NOT NULL | Creation time |
| `update_time` | timestamp | NOT NULL | Modification time |
| `hash_value` | varchar(32) | NOT NULL | response message MD5 hash value |

## 主键 / 索引
- 主键:(`id`)
- 唯一约束:
  - `unique_channel_response` 唯一 (channel_code, response_code, response_sub_code, hash_value)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
