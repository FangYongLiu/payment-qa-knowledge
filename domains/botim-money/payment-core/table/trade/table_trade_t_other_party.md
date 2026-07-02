---
id: tbl_trade_t_other_party
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
- t_other_party
subdomain: trade
module: null
sensitivity: normal
name: 交易其他参与方(t_other_party)
aliases:
- t_other_party
related_services:
- svc_tradeii
related_scenarios: []
---
# 交易其他参与方(t_other_party)

## 用途
交易其他参与方。属 trade 库,由 [[svc_tradeii]] 读写。

## 关联关系
- **所属服务**:[[svc_tradeii]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / NOT NULL | 主建 |
| `trade_voucher_no` | varchar(32) | NOT NULL | 交易凭证号 |
| `party_id` | varchar(32) | NOT NULL | 参与方id |
| `account_type` | varchar(32) | NOT NULL | 账户类型 |
| `account_no` | varchar(32) | NOT NULL | 账户 |
| `party_role` | varchar(32) | NOT NULL | 参与方角色 |
| `amount` | decimal(15,4) | NOT NULL | 支付金额 |
| `fee` | decimal(15,4) | NOT NULL | 费用金额 |
| `currency` | char(3) | NOT NULL | 币种 |
| `party_identity` | varchar(32) |  | 付款方标识 |
| `party_identity_type` | varchar(32) |  | 付款方标识类型 |
| `extension` | varchar(100) |  | 扩展参数 |

## 主键 / 索引
- 主键:(`id`)
- 索引:
  - `t_other_party_trade_voucher_no_index` (trade_voucher_no)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
