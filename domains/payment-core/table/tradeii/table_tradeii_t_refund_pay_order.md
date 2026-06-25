---
id: tbl_tradeii_t_refund_pay_order
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
- refund
- t_refund_pay_order
subdomain: refund
module: null
sensitivity: normal
name: 退付款订单(t_refund_pay_order)
aliases:
- t_refund_pay_order
related_services:
- svc_tradeii
related_scenarios: []
---
# 退付款订单(t_refund_pay_order)

## 用途
退付款订单。属 tradeii 库(交易/支付/退款核心),由 [[svc_tradeii]] 读写。

## 关联关系
- **所属服务**:[[svc_tradeii]](交易核心,= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `refund_pay_voucher_no` | bigint | PK / NOT NULL | 退付款凭证号：18位，固定31+10位时间戳+4位序列+2位随机 |
| `refund_voucher_no` | bigint | NOT NULL | 退款凭证号 |
| `pay_amount` | decimal(19,4) | NOT NULL | 退付款金额 |
| `payable_amount` | decimal(19,4) | NOT NULL | 退法币金额 |
| `return_payer_fee` | decimal(19,4) |  | 退回费用 |
| `currency` | char(3) | NOT NULL | 币种 |
| `pay_channel` | varchar(10) | NOT NULL | 支付渠道 |
| `control_extension` | varchar(128) |  | 控制参数：charger=收费账号，exchangeRate=汇率 |
| `payment_status` | varchar(10) | NOT NULL | 支付状态：P=处理中，S=成功，F=失败 |
| `channel_extension` | varchar(1024) |  | 扩展参数 |
| `unity_result_code` | varchar(50) |  | 统一返回码 |
| `extension` | varchar(1024) |  | 扩展参数 |
| `finish_time` | timestamp(3) |  | 结束时间 |
| `create_time` | timestamp(3) | NOT NULL / 默认 CURRENT_TIMESTAMP(3) | 创建时间 |
| `update_time` | timestamp(3) | NOT NULL / 默认 CURRENT_TIMESTAMP(3) | 修改时间 |

## 主键 / 索引
- 主键:(`refund_pay_voucher_no`)
- 索引:
  - `idx_refund_voucher_no` (refund_voucher_no)
  - `idx_update_time` (update_time)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
