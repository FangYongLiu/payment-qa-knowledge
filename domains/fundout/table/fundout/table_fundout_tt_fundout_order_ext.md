---
id: tbl_fundout_tt_fundout_order_ext
object_type: Table
domain: fundout
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-06-25'
source_type: DB DDL
source_ref: DataGrip DDL export (fundout schema) 2026-06-25
tags:
- fundout
- fundout
- tt_fundout_order_ext
subdomain: fundout
module: null
sensitivity: normal
name: 出款交易订单扩展表(tt_fundout_order_ext)
aliases:
- tt_fundout_order_ext
related_services:
- svc_fundout
related_scenarios: []
---
# 出款交易订单扩展表(tt_fundout_order_ext)

## 用途
出款交易订单扩展表。属 fundout 库,由 [[svc_fundout]] 读写。

## 关联关系
- **所属服务**:[[svc_fundout]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `fundout_order_no` | varchar(32) | PK / NOT NULL | 出款交易凭证号 |
| `client_id` | varchar(32) |  | 调用方标识 |
| `FEE_BEARER` | varchar(32) |  | 费用承担者 |
| `BEARER_ACCOUNT_TYPE` | varchar(32) |  | 费用承担者账户类型 |
| `BEARER_ACCOUNT_NO` | varchar(32) |  | 费用承担者账户号 |
| `SETTLE_DATE` | timestamp |  | 结算时间 |
| `risk_info` | varchar(512) |  | Risk Info |
| `extension` | varchar(255) |  | 扩展字段 |

## 主键 / 索引
- 主键:(`fundout_order_no`)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
