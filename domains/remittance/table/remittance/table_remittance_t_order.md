---
id: tbl_remittance_t_order
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
- t_order
subdomain: remittance
module: null
sensitivity: normal
name: 汇款订单(t_order)
aliases:
- t_order
related_services:
- svc_remittance
related_scenarios: []
---
# 汇款订单(t_order)

## 用途
汇款订单。属 remittance 库,由 [[svc_remittance]] 读写。

## 关联关系
- **所属服务**:[[svc_remittance]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `order_no` | bigint | PK / NOT NULL | 订单号 |
| `relation_order_no` | bigint |  | 关联订单号 |
| `basic_order_no` | bigint |  | 基础订单 |
| `channel_code` | varchar(32) | NOT NULL | 渠道code |
| `payer_id` | varchar(20) | NOT NULL | 付款人 |
| `order_amount` | decimal(19,4) | NOT NULL | 订单金额 |
| `from_amount` | decimal(19,4) | NOT NULL | 汇款金额 |
| `from_currency` | varchar(3) | NOT NULL | 汇款币种 |
| `outer_total_amount` | decimal(19,4) | NOT NULL | 外部总额(包含各种费) |
| `exchange_rate` | varchar(15) | NOT NULL | 汇率 |
| `to_amount` | decimal(19,4) | NOT NULL | 目标金额 |
| `to_currency` | varchar(3) | NOT NULL | 目标币种 |
| `biz_product_code` | varchar(10) | NOT NULL | 产品码 |
| `outer_fee` | decimal(19,4) |  | 外部外扣费用 |
| `outer_fee_currency` | char(3) |  |  |
| `inner_fee` | decimal(19,4) |  | 内部费 |
| `transfer_vat` | decimal(15,4) |  | vat |
| `channel_settle_amount` | decimal(19,4) |  | 渠道结算金额 |
| `channel_settle_currency` | varchar(5) |  | 渠道结算币种 |
| `channel_settle_rate` | varchar(15) |  | 渠道结算汇率 |
| `channel_order_no` | varchar(64) |  | 渠道订单号 |
| `order_status` | varchar(10) | NOT NULL | 状态: WP=等待支付,EC=超时关闭,PS=支付成功,FRP=失败退款中,F=失败,REC=汇款订单已创建,REFC=汇款资金已转换,REP=汇款渠道已出款 |
| `pay_channel` | char(5) |  | 支付渠道 |
| `paid_time` | timestamp |  | 付款成功时间 |
| `remittance_create_time` | char(35) |  | 渠道汇款订单创建时间 |
| `funds_converted_time` | timestamp |  | 汇款金额转换时间 |
| `unity_result_code` | varchar(50) |  | 统一结果码 |
| `extension` | varchar(500) |  | extension |
| `memo` | varchar(100) |  | 备注 |
| `create_time` | timestamp | NOT NULL | 创建时间 |
| `update_time` | timestamp | NOT NULL | 修改时间 |
| `to_country_code` | varchar(10) |  | 目标国家code |
| `channel_return_code` | varchar(20) |  | 渠道返回code |
| `payer_partner_id` | varchar(50) |  | 付款人平台 |
| `payee_id` | varchar(50) |  | 收款人 |
| `order_sub_status` | varchar(20) |  | 子状态 |
| `recipient_id` | bigint |  | 受益人Id |
| `transaction_mode` | varchar(16) | NOT NULL | 汇款模式;CASH_PICK_UP,BANK_TRANSFER,MOBILE_WALLET |
| `rate_income` | decimal(19,4) |  | 汇率加点 |
| `reset_rate` | varchar(15) |  | 重置费率 |
| `diff_income` | decimal(19,4) |  | 重置费率收益 |
| `expire_time` | timestamp |  | 过期时间 |
| `expected_delivery_date` | timestamp |  | 预计交货时间 |
| `refund_order_no` | bigint |  | 退款订单号 |
| `receivable_fee` | decimal(15,4) |  | 应收费用 |
| `recipient_fee` | decimal(15,4) |  | 收款方费用 |
| `finish_time` | timestamp |  | 完成时间 |
| `aml_hold_flag` | char |  | AML hold flag;Y=AML hold，N or NULL=no AML hold |

## 主键 / 索引
- 主键:(`order_no`)
- 索引:
  - `idx_channel_order_no` (channel_order_no)
  - `idx_order_basic_order_no` (basic_order_no)
  - `idx_order_create_time_payer_id` (create_time, payer_id)
  - `idx_order_payer_id` (payer_id)
  - `idx_order_update_time` (update_time)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
