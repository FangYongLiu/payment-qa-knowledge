---
id: tbl_trade_t_acq_trade_order_ext
object_type: Table
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-25'
source_type: DB DDL
source_ref: DataGrip DDL export (trade schema) 2026-06-25
tags:
- trade
- trade
- t_acq_trade_order_ext
subdomain: trade
module: null
sensitivity: normal
name: 收单交易扩展(t_acq_trade_order_ext)
aliases:
- t_acq_trade_order_ext
related_services:
- svc_tradeii
related_scenarios: []
---
# 收单交易扩展(t_acq_trade_order_ext)

## 用途
收单交易扩展。属 trade 库,由 [[svc_tradeii]] 读写。

## 关联关系
- **所属服务**:[[svc_tradeii]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `TRADE_VOUCHER_NO` | varchar(32) | PK / NOT NULL | 交易凭证号 |
| `PROD_DESC` | varchar(1000) |  | 商品信息 |
| `PROD_SHOW_URL` | varchar(256) |  | 商品展示URL |
| `PREPAID_AMOUNT` | decimal(15,4) |  | 下订金额 |
| `PREPAID_VOUCHER_NO` | varchar(32) |  | 下订交易关联凭证号 |
| `COIN_AMOUNT` | decimal(15,4) |  | 金币金额 |
| `ENSURE_AMOUNT` | decimal(15,4) |  | 担保金额 |
| `PAID_AMOUNT` | decimal(15,4) |  | 已付款金额 |
| `SETTLED_AMOUNT` | decimal(15,4) |  | 已结算金额 |
| `GMT_CREATE` | timestamp | NOT NULL / 默认 CURRENT_TIMESTAMP | 创建时间 |
| `GMT_MODIFIED` | timestamp |  | 修改时间 |
| `REFUND_ENSURE_AMOUNT` | decimal(15,4) |  | 退担保金额 |
| `REFUNDED_SETTLE_AMOUNT` | decimal(15,4) |  | 已退结算金额 |
| `REFUNDED_PAY_AMOUNT` | decimal(15,4) |  | 已退付款金额 |
| `CURRENCY` | char(3) |  | 币种 |

## 主键 / 索引
- 主键:(`TRADE_VOUCHER_NO`)
- 索引:
  - `IDX_ATOE_PREPAID_VN` (PREPAID_VOUCHER_NO)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
