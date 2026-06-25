---
id: tbl_remittance_t_flow_difference
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
- t_flow_difference
subdomain: remittance
module: null
sensitivity: normal
name: Reconciliation difference(t_flow_difference)
aliases:
- t_flow_difference
related_services:
- svc_remittance
related_scenarios: []
---
# Reconciliation difference(t_flow_difference)

## 用途
Reconciliation difference。属 remittance 库,由 [[svc_remittance]] 读写。

## 关联关系
- **所属服务**:[[svc_remittance]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint(32) | PK / NOT NULL | id |
| `channel_code` | varchar(10) | NOT NULL | Channel code |
| `inst_order_no` | varchar(32) | NOT NULL | inst order no |
| `bill_date` | char(8) | NOT NULL | bill date |
| `amount` | decimal(19,4) | NOT NULL | amount |
| `currency` | char(3) | NOT NULL | currency |
| `settle_amount` | decimal(19,4) |  | Settle amount |
| `settle_currency` | char(3) |  | Settle currency |
| `status` | char(10) | NOT NULL | Status: INIT,SUCCESS,IGNOR,ERROR |
| `remark` | varchar(120) |  | Remark |
| `extension` | varchar(255) |  | Extension |
| `create_time` | timestamp | NOT NULL | Create time |
| `update_time` | timestamp | NOT NULL | Update time |

## 主键 / 索引
- 主键:(`id`)
- 唯一约束:
  - `uk_channel_inst_order` 唯一 (channel_code, inst_order_no)
- 索引:
  - `idx_update_time` (update_time)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
