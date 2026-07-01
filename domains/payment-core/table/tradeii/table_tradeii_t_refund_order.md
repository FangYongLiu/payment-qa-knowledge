---
id: tbl_tradeii_t_refund_order
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
- t_refund_order
subdomain: trade
module: null
sensitivity: normal
name: 退款订单(t_refund_order)
aliases:
- t_refund_order
related_services:
- svc_tradeii
related_scenarios: []
---
# 退款订单(t_refund_order)

## 用途
退款订单。属 tradeii 库,由 [[svc_tradeii]] 读写。

## 关联关系
- **所属服务**:[[svc_tradeii]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `refund_voucher_no` | bigint | PK / NOT NULL | 退款凭证号：18位，固定13+10位时间戳+4位序列+2位随机 |
| `refund_request_no` | bigint | NOT NULL | 退款请求号 |
| `client_id` | varchar(32) | NOT NULL | 客户端id |
| `trade_voucher_no` | bigint | NOT NULL | 交易凭证号 |
| `refund_payer_id` | varchar(32) |  | 退付款人ID |
| `refund_amount` | decimal(19,4) | NOT NULL | 退款金额 |
| `currency` | char(3) | NOT NULL | 交易币种 |
| `refund_dcc_amount` | decimal(19,4) |  | refund dcc amount |
| `refund_dcc_currency` | char(3) |  | refund dcc currency |
| `refund_type` | varchar(10) |  | 退款类型：CANCEL=取消结算，REFUND=退结算 |
| `control_extension` | varchar(128) |  | 控制参数：reverse=冲正，exchangeSettle=换汇结算，feeUnset=手续费未设置 |
| `refund_status` | varchar(10) | NOT NULL | 退款状态：A=申请中，P=处理中，S=成功，F=失败 |
| `refund_sub_status` | varchar(10) |  | 退款子状态：RS=退结算，RE=退换汇，RP=退付款，RM=退营销，WRP=等待退付款 |
| `unity_result_code` | varchar(50) |  | 统一返回码 |
| `refund_settle_voucher_no` | bigint |  | 退结算订单 |
| `refund_exchange_voucher_no` | bigint |  | 退换汇订单 |
| `refund_pay_voucher_no` | bigint |  | 退付款订单 |
| `refund_installment_voucher_no` | bigint |  | refund installment voucherNo |
| `extension` | varchar(255) |  | 扩展参数 |
| `memo` | varchar(255) |  | 备注 |
| `refund_settle_time` | timestamp |  | 退结算时间 |
| `estimated_time` | timestamp |  | 预计到账时间 |
| `finish_time` | timestamp |  | 结束时间 |
| `create_time` | timestamp | NOT NULL / 默认 CURRENT_TIMESTAMP | 创建时间 |
| `update_time` | timestamp | NOT NULL / 默认 CURRENT_TIMESTAMP | 修改时间 |

## 主键 / 索引
- 主键:(`refund_voucher_no`)
- 索引:
  - `idx_create_time_refund_status` (create_time, refund_status)
  - `idx_refund_request_no` (refund_request_no)
  - `idx_trade_voucher_no` (trade_voucher_no)
  - `idx_update_time_client_id` (update_time, client_id)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
