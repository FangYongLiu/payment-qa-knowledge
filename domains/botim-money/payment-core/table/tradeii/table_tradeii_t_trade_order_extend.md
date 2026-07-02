---
id: tbl_tradeii_t_trade_order_extend
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
- t_trade_order_extend
subdomain: trade
module: null
sensitivity: normal
name: 交易订单扩展(t_trade_order_extend)
aliases:
- t_trade_order_extend
related_services:
- svc_tradeii
related_scenarios: []
---
# 交易订单扩展(t_trade_order_extend)

## 用途
交易订单扩展。属 tradeii 库,由 [[svc_tradeii]] 读写。

## 关联关系
- **所属服务**:[[svc_tradeii]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `trade_voucher_no` | bigint | PK / NOT NULL | 交易凭证号：18位，固定13+10位时间戳+4位序列+2位随机 |
| `description` | varchar(255) | NOT NULL | 商品描述 |
| `cashier_biz_type` | varchar(32) |  | 收银台业务类型 |
| `cashier_payee` | varchar(20) |  | 收银台收款方 |
| `cashier_payee_name` | varchar(100) |  | 收款人名称 |
| `cashier_return_url` | varchar(255) |  | 收银台返回地址 |
| `user_memo` | varchar(128) |  | 用户备注 |
| `bill_extension` | varchar(255) |  | 账单扩展信息 |
| `cashier_extension` | varchar(512) |  | inapp 收银台token参数 |
| `terminal_extension` | varchar(255) |  | Terminal Info |
| `risk_extension` | varchar(512) |  | Risk info |
| `create_time` | timestamp | NOT NULL / 默认 CURRENT_TIMESTAMP | 创建时间 |
| `update_time` | timestamp | NOT NULL / 默认 CURRENT_TIMESTAMP | 修改时间 |

## 主键 / 索引
- 主键:(`trade_voucher_no`)
- 索引:
  - `idx_update_time` (update_time)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
