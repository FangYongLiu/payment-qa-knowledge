---
id: tbl_remittance_t_order_event
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
- t_order_event
subdomain: remittance
module: null
sensitivity: normal
name: 订单事件(t_order_event)
aliases:
- t_order_event
related_services:
- svc_remittance
related_scenarios: []
---
# 订单事件(t_order_event)

## 用途
订单事件。属 remittance 库,由 [[svc_remittance]] 读写。

## 关联关系
- **所属服务**:[[svc_remittance]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / NOT NULL | 主键;8+9 |
| `order_no` | bigint | NOT NULL | 订单号 |
| `config_id` | int |  | 事件配置ID |
| `event_code` | varchar(64) |  | 事件CODE |
| `event_name` | varchar(100) |  | 事件名称 |
| `event_content` | varchar(250) |  | 事件内容 |
| `org_status` | varchar(12) |  | 原状态 |
| `org_sub_status` | varchar(20) |  | 原子状态 |
| `order_status` | varchar(12) |  | 订单状态 |
| `order_sub_status` | varchar(20) |  | 订单子状态 |
| `create_time` | timestamp | NOT NULL | 创建时间 |
| `update_time` | timestamp | NOT NULL | 更新时间 |

## 主键 / 索引
- 主键:(`id`)
- 索引:
  - `idx_order_no_conf_id` (order_no, event_code)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
