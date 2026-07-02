---
id: tbl_remittance_t_hold_order_task
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
- t_hold_order_task
subdomain: remittance
module: null
sensitivity: normal
name: Hold订单Task(t_hold_order_task)
aliases:
- t_hold_order_task
related_services:
- svc_remittance
related_scenarios: []
---
# Hold订单Task(t_hold_order_task)

## 用途
Hold订单Task。属 remittance 库,由 [[svc_remittance]] 读写。

## 关联关系
- **所属服务**:[[svc_remittance]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `task_id` | bigint | PK / NOT NULL | TASK ID;8+9 |
| `relation_id` | varchar(64) |  | 记录ID |
| `channel_code` | varchar(7) | NOT NULL | 渠道CODE |
| `task_type` | char(2) | NOT NULL | 任务类型;RC:风控,RT:退票 |
| `task_mode` | varchar(10) |  | task 模式 |
| `order_no` | bigint | NOT NULL | 订单号 |
| `channel_order_no` | varchar(64) | NOT NULL | 渠道订单号 |
| `hold_on` | varchar(16) | NOT NULL | Hold类型;sender，receiver |
| `transaction_mode` | varchar(30) | NOT NULL | 汇款模式 |
| `from_currency` | char(3) | NOT NULL | 原币种;汇款原币种 |
| `to_country` | char(2) | NOT NULL | 汇款国家;汇款目标国家 |
| `to_currency` | char(3) | NOT NULL | 汇款币种;汇款目标币种 |
| `hold_reason` | varchar(12) | NOT NULL | Hold原因 |
| `status` | char(2) | NOT NULL | 目标国家;P,AS,S,C |
| `unity_code` | varchar(32) |  | 统一code;如退票，订单不存在，订单状态不对 |
| `extension` | varchar(255) |  | 扩展信息 |
| `create_time` | timestamp | NOT NULL | 创建时间 |
| `update_time` | timestamp | NOT NULL | 更新时间 |

## 主键 / 索引
- 主键:(`task_id`)
- 索引:
  - `idx_order_no` (order_no)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
