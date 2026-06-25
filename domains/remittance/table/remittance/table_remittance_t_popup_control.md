---
id: tbl_remittance_t_popup_control
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
- t_popup_control
subdomain: remittance
module: null
sensitivity: normal
name: t_popup_control
aliases:
- t_popup_control
related_services:
- svc_remittance
related_scenarios: []
---
# t_popup_control

## 用途
待补。属 remittance 库,由 [[svc_remittance]] 读写。

## 关联关系
- **所属服务**:[[svc_remittance]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | int | PK / AUTO_INC | Primary Key |
| `member_id` | varchar(20) | NOT NULL | Member ID |
| `business` | varchar(20) | NOT NULL | business type, such as SNPL |
| `pop_times` | tinyint | NOT NULL / 默认 0 | pop count |
| `create_time` | timestamp | 默认 CURRENT_TIMESTAMP | Create time |
| `update_time` | timestamp | 默认 CURRENT_TIMESTAMP | Update time |

## 主键 / 索引
- 主键:(`id`)
- 唯一约束:
  - `member_id` 唯一 (member_id, business)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
