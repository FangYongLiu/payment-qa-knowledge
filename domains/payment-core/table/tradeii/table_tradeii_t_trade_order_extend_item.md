---
id: tbl_tradeii_t_trade_order_extend_item
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
- t_trade_order_extend_item
subdomain: trade
module: null
sensitivity: normal
name: Trade Order Extend Item(t_trade_order_extend_item)
aliases:
- t_trade_order_extend_item
related_services:
- svc_tradeii
related_scenarios: []
---
# Trade Order Extend Item(t_trade_order_extend_item)

## 用途
Trade Order Extend Item。属 tradeii 库,由 [[svc_tradeii]] 读写。

## 关联关系
- **所属服务**:[[svc_tradeii]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `item_id` | bigint | PK / NOT NULL | Item ID |
| `trade_voucher_no` | bigint | NOT NULL | Trade Voucher No |
| `item_type` | varchar(20) | NOT NULL | Item Type |
| `item_code` | varchar(20) | NOT NULL | Item Code |
| `item_value` | varchar(255) | NOT NULL | Item Value |
| `create_time` | timestamp | NOT NULL / 默认 CURRENT_TIMESTAMP | 创建时间 |
| `update_time` | timestamp | NOT NULL / 默认 CURRENT_TIMESTAMP | 修改时间 |

## 主键 / 索引
- 主键:(`item_id`)
- 唯一约束:
  - `uk_trade_voucher_no_type_code` 唯一 (trade_voucher_no, item_type, item_code)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
