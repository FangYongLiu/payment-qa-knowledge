---
id: tbl_remittance_t_notification_event
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
- t_notification_event
subdomain: remittance
module: null
sensitivity: normal
name: 通知事件(t_notification_event)
aliases:
- t_notification_event
related_services:
- svc_remittance
related_scenarios: []
---
# 通知事件(t_notification_event)

## 用途
通知事件。属 remittance 库,由 [[svc_remittance]] 读写。

## 关联关系
- **所属服务**:[[svc_remittance]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `event_id` | bigint | PK / NOT NULL | 主键 |
| `config_id` | int | NOT NULL | 配置id |
| `order_no` | bigint | NOT NULL | 订单号 |
| `member_id` | varchar(20) |  | 会员号 |
| `target_address` | varchar(32) | NOT NULL | 通知目标 |
| `next_time` | timestamp | NOT NULL | 下次通知时间 |
| `success_times` | int |  | 通知成功次数 |
| `status` | varchar(15) | NOT NULL | 状态(PROCESSING - 处理中,FINISHED - 结束, CLOSE - 关闭) |
| `create_time` | timestamp | NOT NULL | 创建时间 |
| `update_time` | timestamp | NOT NULL | 修改时间 |

## 主键 / 索引
- 主键:(`event_id`)
- 索引:
  - `idx_not_eve_con_id` (config_id)
  - `idx_not_eve_ord_no` (order_no)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
