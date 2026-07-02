---
id: tbl_tradeii_t_trade_marketing
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
- t_trade_marketing
subdomain: trade
module: null
sensitivity: normal
name: 交易营销(t_trade_marketing)
aliases:
- t_trade_marketing
related_services:
- svc_tradeii
related_scenarios: []
---
# 交易营销(t_trade_marketing)

## 用途
交易营销。属 tradeii 库,由 [[svc_tradeii]] 读写。

## 关联关系
- **所属服务**:[[svc_tradeii]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `trade_marketing_id` | bigint | PK / NOT NULL | 交易营销id：前八后九 |
| `voucher_no` | bigint | NOT NULL | 凭证号 |
| `order_type` | varchar(10) | NOT NULL | 订单类型：P=付款，R=退款 |
| `market_method_type` | varchar(10) | NOT NULL | 营销方式类型：CUT=优惠券，GP=GreenPoint |
| `amount` | decimal(19,4) | NOT NULL | 抵扣金额 |
| `undo_amount` | decimal(19,4) |  | 取消金额 |
| `currency` | char(3) | NOT NULL | 币种 |
| `market_status` | varchar(10) | NOT NULL | 营销状态：I=初始，FP=冻结中，FS=冻结成功，SS=结算成功，冻结失败=FF，撤销成功=CS，已取消=C，RP=退回中，RS=退成功 |
| `account_no` | varchar(32) |  | 资金账户 |
| `unity_result_code` | varchar(50) |  | 统一返回码 |
| `extension` | varchar(255) |  | 扩展参数 |
| `create_time` | timestamp | NOT NULL / 默认 CURRENT_TIMESTAMP | 创建时间 |
| `paid_time` | timestamp |  | 冻结成功时间 |
| `update_time` | timestamp | NOT NULL / 默认 CURRENT_TIMESTAMP | 修改时间 |

## 主键 / 索引
- 主键:(`trade_marketing_id`)
- 索引:
  - `idx_voucher_no` (voucher_no)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
