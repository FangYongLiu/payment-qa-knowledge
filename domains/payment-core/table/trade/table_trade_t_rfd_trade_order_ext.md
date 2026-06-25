---
id: tbl_trade_t_rfd_trade_order_ext
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
- t_rfd_trade_order_ext
subdomain: trade
module: null
sensitivity: normal
name: 退款交易扩展(t_rfd_trade_order_ext)
aliases:
- t_rfd_trade_order_ext
related_services:
- svc_tradeii
related_scenarios: []
---
# 退款交易扩展(t_rfd_trade_order_ext)

## 用途
退款交易扩展。属 trade 库,由 [[svc_tradeii]] 读写。

## 关联关系
- **所属服务**:[[svc_tradeii]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `TRADE_VOUCHER_NO` | varchar(32) | PK / NOT NULL | 交易凭证号 |
| `REFUND_ENSURE_AMOUNT` | decimal(15,4) |  | 退担保金额 |
| `REFUND_COIN_AMOUNT` | decimal(15,4) |  | 退金币金额 |
| `REFUND_PREPAY_AMOUNT` | decimal(15,4) |  | 退订金金额 |
| `REFUND_SETTLED_AMOUNT` | decimal(15,4) |  | 已退结算金额 |
| `REFUND_PAID_AMOUNT` | decimal(15,4) |  | 已退付款金额 |
| `MEMO` | varchar(128) |  | 备注 |
| `GMT_CREATE` | timestamp | NOT NULL / 默认 CURRENT_TIMESTAMP | 创建时间 |
| `GMT_MODIFIED` | timestamp |  | 修改时间 |
| `CURRENCY` | char(3) |  | 币种 |

## 主键 / 索引
- 主键:(`TRADE_VOUCHER_NO`)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
