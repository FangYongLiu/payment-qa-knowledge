---
id: tbl_remittance_t_basic_order
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
- t_basic_order
subdomain: remittance
module: null
sensitivity: normal
name: 汇款订单(t_basic_order)
aliases:
- t_basic_order
related_services:
- svc_remittance
related_scenarios: []
---
# 汇款订单(t_basic_order)

## 用途
汇款订单。属 remittance 库,由 [[svc_remittance]] 读写。

## 关联关系
- **所属服务**:[[svc_remittance]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `basic_order_no` | bigint | PK / NOT NULL | 订单号 |
| `channel_code` | varchar(32) | NOT NULL | 渠道code |
| `payer_id` | varchar(20) | NOT NULL | 付款人 |
| `order_amount` | decimal(19,4) | NOT NULL | 订单金额 |
| `from_amount` | decimal(19,4) | NOT NULL | 汇款金额 |
| `from_currency` | char(3) | NOT NULL | 汇款币种 |
| `outer_total_amount` | decimal(19,4) | NOT NULL | 外部总额(包含各种费) |
| `exchange_rate` | varchar(15) | NOT NULL | 汇率 |
| `to_amount` | decimal(19,4) | NOT NULL | 目标金额 |
| `to_currency` | char(3) | NOT NULL | 目标币种 |
| `biz_product_code` | varchar(10) | NOT NULL | 产品码 |
| `outer_fee` | decimal(19,4) |  | 外部外扣费用 |
| `outer_fee_currency` | char(3) |  |  |
| `inner_fee` | decimal(19,4) |  | 内部费 |
| `transfer_vat` | decimal(15,4) |  | vat |
| `channel_settle_amount` | —(DDL未定义) |  |  |
| `channel_settle_currency` | —(DDL未定义) |  |  |
| `channel_settle_rate` | —(DDL未定义) |  |  |
| `channel_order_no` | varchar(32) |  | 渠道订单号 |
| `remittance_create_time` | timestamp |  | 渠道汇款订单创建时间 |
| `extension` | varchar(255) |  | 扩展参数 |
| `create_time` | timestamp | NOT NULL | 创建时间 |
| `update_time` | timestamp | NOT NULL | 修改时间 |
| `to_country_code` | char(3) |  | 目标国家code |
| `payer_partner_id` | varchar(50) |  | 付款人平台 |
| `recipient_id` | bigint |  | 受益人Id |
| `transaction_mode` | varchar(20) |  | 汇款模式;CASH_PICK_UP,BANK_TRANSFER,MOBILE_WALLET |
| `rate_income` | decimal(19,4) |  | 汇率加点 |
| `reset_rate` | varchar(15) |  | 重置费率 |
| `diff_income` | decimal(19,4) |  | 重置费率收益 |
| `expire_time` | timestamp |  | 过期时间 |
| `receivable_fee` | decimal(15,4) |  | 应收费用 |
| `recipient_fee` | decimal(15,4) |  | 收款方费用 |
| `recipient_fee_currency` | char(3) |  | 收款方费用币种 |

## 主键 / 索引
- 主键:(`basic_order_no`)
- 索引:
  - `idx_channel_order_no` (channel_order_no)
  - `idx_order_update_time` (update_time)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
