---
id: tbl_transferii_t_wallet_order
object_type: Table
name: 钱包订单主表 (t_wallet_order)
aliases: [t_wallet_order, Wallet Order]
domain: wallet
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-06-25'
source_type: wiki
source_ref: wiki_image:654d5bef-1e1a-485d-a44b-c83918b7165b
tags: [transferii, send-money, wallet-order]
related_services: [svc_transfer]
related_scenarios: []
---

# 钱包订单主表 (t_wallet_order)

## 用途
位于 `transferii` schema,是 Send Money(Wallet Redesign)数据模型的核心订单主表。一笔 wallet_order 对应多个参与方订单([[tbl_transferii_t_party_order]])、收款凭证([[tbl_transferii_t_order_permit]])与取消记录([[tbl_transferii_t_cancel_order]])。流程见 [[flow_wallet_send_money]]。

> 所属服务:[[svc_transfer]](wallet 域个人转账)。

## 关联关系
- **所属服务**:transfer(待补,未建 Service 对象)
- **子表(通过 `wallet_order_no` 作 FK 关联)**:[[tbl_transferii_t_party_order]]、[[tbl_transferii_t_order_permit]]、[[tbl_transferii_t_cancel_order]]
- **校验它的流程**:[[flow_wallet_send_money]]

## 关键列
| 列名 | 标签 | 键 | 类型 | 长度 |
|---|---|---|---|---|
| wallet_order_no | Wallet Order No | PK | varchar | 32 |
| order_type | Order Type | | char | 2 |
| partner_id | Partner ID | | varchar | 20 |
| member_id | Member ID | | varchar | 20 |
| order_amount | Order Amount | | decimal | 19,4 |
| party_count | Party Count | | int | |
| currency | Currency | | char | 3 |
| status | Status | | char | 2 |
| expire_time | Expire Time | | timestamp | |
| trade_extension | Trade Extension | | varchar | 255 |

## 主键 / 索引
- 主键:`wallet_order_no`(varchar(32))
- 被以下表通过 `wallet_order_no` 作 FK 关联:`t_party_order`、`t_order_permit`、`t_cancel_order`(后者原文字段被截断)。

## 校验点(QA 关注)
- `wallet_order_no` 全局唯一,且与子表 FK 一致。
- `order_amount` 精度 decimal(19,4);`currency` char(3) 须符合 ISO 货币码长度。
- `party_count` 应与实际生成的 `t_party_order` 行数匹配。
- `status`(char(2))、`order_type`(char(2)) 取值需对齐枚举(原文未列出具体取值,待补)。
- `expire_time` 用于订单过期控制,需与取消/失效流程(`t_cancel_order`)行为一致。
- `partner_id`(20) 与 `t_party_order.partner_id`(32) 长度不同,跨表比对/写入时注意截断与一致性。
- `trade_extension` varchar(255) 作为扩展字段,关注长度上限与 JSON/编码规范。
