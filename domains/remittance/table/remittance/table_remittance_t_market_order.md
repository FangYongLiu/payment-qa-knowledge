---
id: tbl_remittance_t_market_order
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
- t_market_order
subdomain: remittance
module: null
sensitivity: normal
name: 营销订单(t_market_order)
aliases:
- t_market_order
related_services:
- svc_remittance
related_scenarios: []
---
# 营销订单(t_market_order)

## 用途
营销订单。属 remittance 库,由 [[svc_remittance]] 读写。

## 关联关系
- **所属服务**:[[svc_remittance]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `market_id` | bigint | PK / NOT NULL | primary key |
| `order_no` | bigint | NOT NULL | 订单号 |
| `market_method` | varchar(7) | NOT NULL | 营销方式 |
| `market_keyword` | varchar(32) | NOT NULL | 营销关键字 |
| `deduct_target` | varchar(20) |  | 抵扣目标，fee（费用）,capital（本金） |
| `amount` | decimal(15,4) |  | 优惠金额 |
| `currency` | char(3) |  | 币种 |
| `account_no` | varchar(32) |  | 资金账号 |
| `market_status` | varchar(7) |  | 营销状态 |
| `extension` | varchar(255) |  | 扩展信息 |
| `create_time` | timestamp | NOT NULL | 创建时间 |
| `update_time` | timestamp | NOT NULL | 修改时间 |

## 主键 / 索引
- 主键:(`market_id`)
- 索引:
  - `idx_order_no` (order_no)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
