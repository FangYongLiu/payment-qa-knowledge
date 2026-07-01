---
id: tbl_remittance_t_corridor_msg_config
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
- t_corridor_msg_config
subdomain: remittance
module: null
sensitivity: normal
name: corridor msg key(t_corridor_msg_config)
aliases:
- t_corridor_msg_config
related_services:
- svc_remittance
related_scenarios: []
---
# corridor msg key(t_corridor_msg_config)

## 用途
corridor msg key。属 remittance 库,由 [[svc_remittance]] 读写。

## 关联关系
- **所属服务**:[[svc_remittance]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | int(10) | PK / AUTO_INC | id |
| `channel_code` | varchar(12) | NOT NULL | Channel code |
| `response_code` | varchar(20) |  | Response code |
| `response_sub_code` | varchar(32) |  | Response sub code |
| `response_msg` | varchar(255) |  | Response message |
| `i18n_key` | varchar(50) |  | Internationalization key |
| `create_time` | timestamp | NOT NULL / 默认 CURRENT_TIMESTAMP | Creation time |
| `update_time` | timestamp | NOT NULL / 默认 CURRENT_TIMESTAMP | Update time |

## 主键 / 索引
- 主键:(`id`)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
