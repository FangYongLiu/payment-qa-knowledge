---
id: tbl_tradeii_t_payment_relate_order
object_type: Table
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-25'
source_type: DB DDL
source_ref: DataGrip DDL export (tradeii schema) 2026-06-25
tags:
- tradeii
- trade
- t_payment_relate_order
subdomain: trade
module: null
sensitivity: normal
name: 支付关联订单(t_payment_relate_order)
aliases:
- t_payment_relate_order
related_services:
- svc_tradeii
related_scenarios: []
---
# 支付关联订单(t_payment_relate_order)

## 用途
支付关联订单。属 tradeii 库,由 [[svc_tradeii]] 读写。

## 关联关系
- **所属服务**:[[svc_tradeii]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `payment_voucher_no` | bigint | PK / NOT NULL | 支付凭证号：18位，固定31+10位时间戳+4位序列+2位随机 |
| `payment_relate_type` | varchar(10) | NOT NULL | 关联类型：AC=自动撤销，MC=手动撤销，AS=自动结算，MS=手动结算，RS=退结算 |
| `relate_voucher_no` | bigint | NOT NULL | 关联凭证号 |
| `trade_voucher_no` | bigint | NOT NULL | 交易凭证号 |
| `payment_status` | varchar(10) | NOT NULL | 状态：P=处理中，S=成功，F=失败 |
| `unity_result_code` | varchar(50) |  | 统一返回码 |
| `create_time` | timestamp | NOT NULL / 默认 CURRENT_TIMESTAMP | 创建时间 |
| `update_time` | timestamp | NOT NULL / 默认 CURRENT_TIMESTAMP | 修改时间 |

## 主键 / 索引
- 主键:(`payment_voucher_no`)
- 索引:
  - `idx_relate_voucher_no` (relate_voucher_no)
  - `idx_trade_voucher_no` (trade_voucher_no)
  - `idx_update_time` (update_time)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
