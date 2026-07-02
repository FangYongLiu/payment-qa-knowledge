---
id: tbl_trade_t_order_ext
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
- t_order_ext
subdomain: trade
module: null
sensitivity: normal
name: 交易扩展表(t_order_ext)
aliases:
- t_order_ext
related_services:
- svc_tradeii
related_scenarios: []
---
# 交易扩展表(t_order_ext)

## 用途
交易扩展表。属 trade 库,由 [[svc_tradeii]] 读写。

## 关联关系
- **所属服务**:[[svc_tradeii]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `TRADE_VOUCHER_NO` | varchar(32) | PK / NOT NULL |  |
| `GMT_AUTO_SETTLE` | timestamp |  | 自动结算时间 |
| `EXTENSION` | varchar(512) |  | 扩展 |
| `GMT_CREATE` | timestamp | NOT NULL | 创建时间 |
| `GMT_MODIFIED` | timestamp |  | 修改时间 |
| `client_id` | varchar(32) |  | 调用方标识 |
| `unity_result_code` | varchar(50) |  | 存储后台服务响应统一结果返回码用于查询、通知 |
| `gmt_auto_settle_trade` | timestamp |  | 记录调用css服务的结算时间不做更新 |

## 主键 / 索引
- 主键:(`TRADE_VOUCHER_NO`)
- 索引:
  - `IDX_OEXT_GMT_AS` (GMT_AUTO_SETTLE)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
