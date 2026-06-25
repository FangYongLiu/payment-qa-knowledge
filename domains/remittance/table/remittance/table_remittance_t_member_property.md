---
id: tbl_remittance_t_member_property
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
- t_member_property
subdomain: remittance
module: null
sensitivity: normal
name: member property(t_member_property)
aliases:
- t_member_property
related_services:
- svc_remittance
related_scenarios: []
---
# member property(t_member_property)

## 用途
member property。属 remittance 库,由 [[svc_remittance]] 读写。

## 关联关系
- **所属服务**:[[svc_remittance]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / AUTO_INC | id |
| `member_id` | varchar(20) | NOT NULL | member id |
| `property_category` | varchar(32) | NOT NULL | Primary Category: LAST_ORDER |
| `property_type` | varchar(15) |  | Type: MG |
| `property_value` | varchar(32) | NOT NULL | value:131xxxx |
| `extension` | varchar(255) |  | extension |
| `create_time` | timestamp | NOT NULL | Create time |
| `update_time` | timestamp | NOT NULL | Update time |

## 主键 / 索引
- 主键:(`id`)
- 唯一约束:
  - `uk_me_cat_type` 唯一 (member_id, property_category, property_type)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
