---
id: tbl_transferii_t_party_order
object_type: Table
name: 参与方订单表 (t_party_order)
aliases: [t_party_order, transferii.t_party_order]
domain: wallet
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-06-25'
source_type: wiki
source_ref: wiki_image:654d5bef-1e1a-485d-a44b-c83918b7165b
tags: [transferii, send-money, party-order]
related_services: [svc_transfer]
related_scenarios: []
---

# 参与方订单表 (t_party_order)

## 用途
位于 `transferii` schema,记录钱包订单([[tbl_transferii_t_wallet_order]])下各参与方(收方/付方)的子订单明细。一笔 wallet_order 可对应多条 party_order,由主表 `party_count` 体现数量。流程见 [[flow_wallet_send_money]]。

## 关联关系
- **所属服务**:transfer(待补,未建 Service 对象)
- **关联主表**:[[tbl_transferii_t_wallet_order]](`wallet_order_no` FK)
- **同模型表**:[[tbl_transferii_t_order_permit]]、[[tbl_transferii_t_cancel_order]]

## 关键列
| 列名 | 类型 | 说明 |
|---|---|---|
| party_order_no | bigint | 参与方订单号(主键) |
| wallet_order_no | bigint(FK) | 关联主表 `t_wallet_order.wallet_order_no` |
| request_no | varchar(64) | 请求号 |
| partner_id | varchar(32) | 合作方 ID |
| member_id | varchar(20) | 会员 ID |
| party_type | char(2) | 参与方类型(区分收方/付方等角色) |
| trade_amount | decimal(19,4) | 交易金额 |
| currency | char(3) | 币种 |
| status | varchar(32) | 参与方订单状态 |
| trade_request_no | bigint | 交易请求号 |

## 主键 / 索引
- 主键:`party_order_no`
- 外键:`wallet_order_no` → `t_wallet_order.wallet_order_no`

## 校验点(QA 关注)
- `wallet_order_no` 必须能在 `t_wallet_order` 中找到对应主单。
- 同一 `wallet_order_no` 下 party_order 条数应与主单 `party_count` 一致。
- `party_type` 取值应覆盖收/付方角色,且与主单 `order_type` 语义一致。
- `trade_amount` / `currency` 应与主单 `order_amount` / `currency` 在业务规则下对账一致。
- 注意 `party_order.partner_id`(32) 与主单 partner_id(20)、`party_order.status`(varchar32) 与主单 status(char2) 长度/编码不一致,关注截断与状态机映射。
- `request_no` / `trade_request_no` 的幂等性与去重校验。
