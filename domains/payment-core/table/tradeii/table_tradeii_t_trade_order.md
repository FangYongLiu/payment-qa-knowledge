---
id: tbl_tradeii_t_trade_order
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
- t_trade_order
subdomain: trade
module: null
sensitivity: normal
name: 交易订单(t_trade_order)
aliases:
- t_trade_order
related_services:
- svc_tradeii
related_scenarios: []
---
# 交易订单(t_trade_order)

## 用途
交易订单。属 tradeii 库,由 [[svc_tradeii]] 读写。

## 关联关系
- **所属服务**:[[svc_tradeii]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `trade_voucher_no` | bigint | PK / NOT NULL | 交易凭证号：18位，固定13+10位时间戳+4位序列+2位随机 |
| `trade_request_no` | bigint | NOT NULL | 交易请求号 |
| `client_id` | varchar(32) | NOT NULL | 客户端id |
| `deduct_type` | varchar(10) | NOT NULL | 扣款类型：C=收银台交易，A=授权交易，I=内部交易 |
| `payer_id` | varchar(20) |  | 付款方ID |
| `trade_amount` | decimal(19,4) |  | 交易金额 |
| `pay_trade_amount` | decimal(19,4) |  | Trade amount to be paid |
| `currency` | char(3) |  | 交易币种 |
| `biz_product_code` | varchar(10) | NOT NULL | 业务产品码 |
| `trade_category` | varchar(32) |  | 交易分类 |
| `partner_id` | varchar(20) | NOT NULL | 合作方ID |
| `control_extension` | varchar(255) |  | Control Parameters：paySettle=Pay Settlement，manualSettle=Manual Settlement，noSettleFee=No Settlement Fee，transferRule=Transfer Rule，reverse=Reversal，exchangeSettle=Exchange Settlement |
| `trade_status` | varchar(10) | NOT NULL | 交易状态：W=等待付款，PS=付款成功，C=关闭，CS=撤销成功，SS=结算成功，PF=付款失败 |
| `trade_sub_status` | varchar(10) |  | 交易子状态：I=初始，S=成功，CP=撤销处理中，SMP=手动结算中，SI=结算初始化，EP=换汇中，SW=等待结算，SP=结算中 |
| `pay_voucher_no` | bigint |  | 付款凭证号 |
| `exchange_voucher_no` | bigint |  | 换汇凭证号 |
| `settle_voucher_no` | bigint |  | 结算凭证号 |
| `unity_result_code` | varchar(50) |  | 统一返回码 |
| `last_fail_unity_result_code` | varchar(64) |  | last fail unity result code |
| `last_fail_pay_voucher_no` | bigint |  | last fail pay voucher no |
| `extension` | varchar(255) |  | 扩展参数 |
| `expire_time` | timestamp |  | 过期时间 |
| `settle_book_time` | timestamp |  | 预计结算时间 |
| `finish_time` | timestamp(3) |  | 结束时间 |
| `create_time` | timestamp(3) | NOT NULL / 默认 CURRENT_TIMESTAMP(3) | 创建时间 |
| `update_time` | timestamp(3) | NOT NULL / 默认 CURRENT_TIMESTAMP(3) | 修改时间 |

## 主键 / 索引
- 主键:(`trade_voucher_no`)
- 索引:
  - `idx_expire_time` (expire_time)
  - `idx_settle_book_time` (settle_book_time)
  - `idx_trade_request_no` (trade_request_no)
  - `idx_update_time_client_id` (update_time, client_id)
  - `idx_update_time_status` (update_time, trade_status)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
