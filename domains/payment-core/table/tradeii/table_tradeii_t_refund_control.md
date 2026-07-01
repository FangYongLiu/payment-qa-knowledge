---
id: tbl_tradeii_t_refund_control
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
- t_refund_control
subdomain: trade
module: null
sensitivity: normal
name: 退款控制(t_refund_control)
aliases:
- t_refund_control
related_services:
- svc_tradeii
related_scenarios: []
---
# 退款控制(t_refund_control)

## 用途
退款控制。属 tradeii 库,由 [[svc_tradeii]] 读写。

## 关联关系
- **所属服务**:[[svc_tradeii]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `control_id` | bigint | PK / NOT NULL | 控制ID：前八后九 |
| `trade_voucher_no` | bigint | NOT NULL | 交易凭证号 |
| `trade_amount` | decimal(19,4) | NOT NULL | 交易金额 |
| `refundable_amount` | decimal(19,4) | NOT NULL | 可退款金额 |
| `currency` | char(3) | NOT NULL | 交易币种 |
| `create_time` | timestamp | NOT NULL / 默认 CURRENT_TIMESTAMP | 创建时间 |
| `update_time` | timestamp | NOT NULL / 默认 CURRENT_TIMESTAMP | 修改时间 |

## 主键 / 索引
- 主键:(`control_id`)
- 索引:
  - `idx_trade_voucher_no` (trade_voucher_no)
  - `idx_update_time` (update_time)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
