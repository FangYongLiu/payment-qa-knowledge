---
id: tbl_tradeii_t_trade_party
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
- t_trade_party
subdomain: trade
module: null
sensitivity: normal
name: 交易参与方(t_trade_party)
aliases:
- t_trade_party
related_services:
- svc_tradeii
related_scenarios: []
---
# 交易参与方(t_trade_party)

## 用途
交易参与方。属 tradeii 库(交易/支付/退款核心),由 [[svc_tradeii]] 读写。

## 关联关系
- **所属服务**:[[svc_tradeii]](交易核心,= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `trade_party_id` | bigint | PK / NOT NULL | 交易参与方id：前八后九 |
| `voucher_no` | bigint | NOT NULL | 凭证号 |
| `order_type` | varchar(10) | NOT NULL | 订单类型：T=交易 |
| `party_role` | varchar(20) | NOT NULL | 参与方角色：payee=收款方，splitPayer=分账付款方，splitPayee=分账收款方，platform=平台方，charger=收费 |
| `member_id` | varchar(20) | NOT NULL | 会员号 |
| `account_no` | varchar(32) | NOT NULL | 账户号 |
| `amount` | decimal(19,4) | NOT NULL | 金额 |
| `fee` | decimal(19,4) |  | 费用 |
| `undo_amount` | decimal(19,4) | NOT NULL | 取消金额 |
| `undo_fee` | decimal(19,4) |  | 取消费用 |
| `currency` | char(3) | NOT NULL | 币种 |
| `memo` | varchar(50) |  | 备注 |
| `extension` | varchar(255) |  | 扩展参数 |
| `create_time` | timestamp | NOT NULL / 默认 CURRENT_TIMESTAMP | 创建时间 |
| `update_time` | timestamp | NOT NULL / 默认 CURRENT_TIMESTAMP | 修改时间 |

## 主键 / 索引
- 主键:(`trade_party_id`)
- 索引:
  - `idx_voucher_no` (voucher_no)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
