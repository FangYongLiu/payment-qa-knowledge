---
id: tbl_remittance_t_refund_order
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
- t_refund_order
subdomain: remittance
module: null
sensitivity: normal
name: 退款订单表(t_refund_order)
aliases:
- t_refund_order
related_services:
- svc_remittance
related_scenarios: []
---
# 退款订单表(t_refund_order)

## 用途
退款订单表。属 remittance 库,由 [[svc_remittance]] 读写。

## 关联关系
- **所属服务**:[[svc_remittance]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `refund_order_no` | bigint | PK / NOT NULL | 退款订单号 |
| `order_no` | bigint | NOT NULL | 原订单号 |
| `mid` | varchar(20) |  | 会员id |
| `refund_amount` | decimal(19,4) | NOT NULL | 退款金额 |
| `refund_fee` | decimal(19,4) |  | 退费 |
| `currency` | char(3) | NOT NULL | 币种 |
| `channel_refund_date_time` | varchar(35) |  | 渠道退款时间 |
| `status` | char | NOT NULL | 退款状态: P-退款中，S-退款成功，F-退款失败 |
| `charge_back_status` | varchar(64) |  | 拒付状态描述-Refund：风控退；Finished with compensation：银行退 |
| `cancel_control` | char(2) |  | 退款方式，Operater Manual(OM)-运营发起, User Manual(UM)-用户发起, Auto(AT)-系统自动发起，Risk Case(RC)-风控事件 |
| `unity_result_code` | varchar(50) |  | 统一错误码 |
| `create_time` | timestamp | NOT NULL | 创建时间 |
| `update_time` | timestamp | NOT NULL | 修改时间 |
| `refund_type` | char(2) |  | 退款类型(C:CANCEL,R:REFUND) |
| `buy_rate` | decimal(19,8) |  | 购买汇率 |
| `revaluation_rate` | decimal(19,8) |  | Revaluation Rate |
| `refund_destination` | varchar(25) |  | Anticipated Refund Destination |

## 主键 / 索引
- 主键:(`refund_order_no`)
- 索引:
  - `idx_order_no` (order_no)
  - `idx_update_time` (update_time)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
