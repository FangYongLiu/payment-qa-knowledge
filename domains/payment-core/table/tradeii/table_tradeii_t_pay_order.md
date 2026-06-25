---
id: tbl_tradeii_t_pay_order
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
- t_pay_order
subdomain: trade
module: null
sensitivity: normal
name: 付款订单(t_pay_order)
aliases:
- t_pay_order
related_services:
- svc_tradeii
related_scenarios: []
---
# 付款订单(t_pay_order)

## 用途
付款订单。属 tradeii 库,由 [[svc_tradeii]] 读写。

## 关联关系
- **所属服务**:[[svc_tradeii]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `pay_voucher_no` | bigint | PK / NOT NULL | 付款凭证号：18位，固定31+10位时间戳+4位序列+2位随机 |
| `trade_voucher_no` | bigint | NOT NULL | 交易凭证号 |
| `client_id` | varchar(32) | NOT NULL | 客户端id |
| `pay_scene` | varchar(20) |  | 支付场景 |
| `pay_entrance` | varchar(32) | NOT NULL | 支付入口 |
| `payer_id` | varchar(32) |  | 付款人 |
| `verify_items` | varchar(128) | NOT NULL | 验证项 |
| `pay_amount` | decimal(19,4) | NOT NULL | 付款金额 |
| `payable_amount` | decimal(19,4) | NOT NULL | 应付金额 |
| `payer_fee` | decimal(19,4) | NOT NULL | 付款方费用 |
| `currency` | char(3) | NOT NULL | 币种 |
| `dcc_markup_amount` | decimal(19,4) |  | dcc markup amount |
| `dcc_total_amount` | decimal(19,4) |  | dcc total amount |
| `dcc_currency` | char(3) |  | dcc currency |
| `dcc_extension` | varchar(255) |  | dcc extension |
| `pay_channel` | varchar(10) | NOT NULL | 支付渠道 |
| `pay_mode` | varchar(20) | NOT NULL | 支付模式 |
| `pay_props` | varchar(255) |  | 付款属性 |
| `pay_funds_extension` | varchar(1024) |  | 付款渠道参数 |
| `channel_extension` | varchar(1024) |  | 扩展参数 |
| `control_extension` | varchar(128) |  | 控制参数：lastPay=最终付款，useMarket=使用营销，charger=收费账号，exchangeRate=汇率 |
| `pay_status` | varchar(10) | NOT NULL | 支付状态：P=处理中，S=成功，F=失败，MP=营销处理中，CP=撤销中，CS=撤销成功 |
| `unity_result_code` | varchar(50) |  | 统一返回码 |
| `cancel_voucher_no` | bigint |  | 撤销凭证号 |
| `extension` | varchar(1024) |  | 扩展参数 |
| `paid_time` | timestamp(3) |  | 付款成功时间 |
| `finish_time` | timestamp(3) |  | 结束时间 |
| `create_time` | timestamp(3) | NOT NULL / 默认 CURRENT_TIMESTAMP(3) | 创建时间 |
| `update_time` | timestamp(3) | NOT NULL / 默认 CURRENT_TIMESTAMP(3) | 修改时间 |

## 主键 / 索引
- 主键:(`pay_voucher_no`)
- 索引:
  - `idx_trade_voucher_no` (trade_voucher_no)
  - `idx_update_time_payer_id` (update_time, payer_id)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
