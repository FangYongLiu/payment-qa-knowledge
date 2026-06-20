---
id: tbl_transferii_t_wallet_order
object_type: Table
domain: fund-out-transfer
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-20'
source_type: wiki_image
source_ref: wiki_image:654d5bef-1e1a-485d-a44b-c83918b7165b
tags:
- send-money
- wallet-order
- schema
subdomain: send-money
module: wallet-order
sensitivity: normal
name: 钱包订单主表 t_wallet_order
aliases:
- t_wallet_order
- Wallet Order
related_services: []
related_tables:
- tbl_transferii_t_party_order
- tbl_transferii_t_order_permit
- tbl_transferii_t_cancel_order
related_scenarios:
- wallet-redesign-send-money-er
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
Send Money 场景下的钱包订单主表，位于 `transferii` schema，记录一笔钱包订单的整体信息：订单类型、发起方、金额、币种、参与方数量、状态以及过期时间等。是 `t_party_order`、`t_order_permit`、`t_cancel_order` 等子表的关联主表。

## 关键列
| 列名 | 标签 | 键 | 类型 | 长度 |
|---|---|---|---|---|
| wallet_order_no | Wallet Order No | PK | varchar | 32 |
| order_type | Order Type |  | char | 2 |
| partner_id | Partner ID |  | varchar | 20 |
| member_id | Member ID |  | varchar | 20 |
| order_amount | Order Amount |  | decimal | 19,4 |
| party_count | Party Count |  | int |  |
| currency | Currency |  | char | 3 |
| status | Status |  | char | 2 |
| expire_time | Expire Time |  | timestamp |  |
| trade_extension | Trade Extension |  | varchar | 255 |

## 主键/索引
- PK：`wallet_order_no`(varchar(32))
- 被以下表通过 `wallet_order_no` 作为 FK 关联：
  - [[tbl_transferii_t_order_permit]](`t_order_permit.wallet_order_no`)
  - [[tbl_transferii_t_party_order]](`t_party_order.wallet_order_no`)
  - [[tbl_transferii_t_cancel_order]](通过 `wallet_order_no` 关联，原文该表字段被截断)

## 校验点(QA 关注)
- `wallet_order_no` 全局唯一，且与子表 `t_party_order` / `t_order_permit` / `t_cancel_order` 的 FK 一致。
- `order_amount` 精度为 decimal(19,4)；`currency` 为 char(3)，需符合 ISO 货币码长度。
- `party_count` 应与实际生成的 `t_party_order` 行数匹配。
- `status`(char(2))、`order_type`(char(2)) 取值需对齐枚举(原文未列出具体取值)。
- `expire_time` 用于订单过期控制，需与取消/失效流程(`t_cancel_order`)行为一致。
- `partner_id`(20) 与 `t_party_order.partner_id`(32) 长度不同，跨表比对/写入时注意截断与一致性。
- `trade_extension` varchar(255)，作为扩展字段需关注长度上限与 JSON/编码规范。
