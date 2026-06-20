---
id: tbl_transferii_t_party_order
object_type: Table
domain: fund-out-transfer
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-20'
source_type: wiki_image
source_ref: wiki_image:654d5bef-1e1a-485d-a44b-c83918b7165b
tags:
- schema:transferii
- send-money
subdomain: wallet-redesign
module: send-money
sensitivity: normal
name: 参与方订单表 t_party_order
aliases:
- transferii.t_party_order
related_services: []
related_tables:
- tbl_transferii_t_wallet_order
- tbl_transferii_t_order_permit
- tbl_transferii_t_cancel_order
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
位于 `transferii` schema 下，记录钱包订单 (`t_wallet_order`) 下各参与方（收方/付方）的子订单明细。一笔 wallet_order 可对应多条 party_order，由 `t_wallet_order.party_count` 体现参与方数量。

## 关键列
- `party_order_no` (bigint)：参与方订单号，主键
- `wallet_order_no` (bigint, FK)：关联主表 `t_wallet_order.wallet_order_no`
- `request_no` (varchar/64)：请求号
- `partner_id` (varchar/32)：合作方 ID
- `member_id` (varchar/20)：会员 ID
- `party_type` (char/2)：参与方类型（区分收方/付方等角色）
- `trade_amount` (decimal/19,4)：交易金额
- `currency` (char/3)：币种
- `status` (varchar/32)：参与方订单状态
- `trade_request_no` (bigint)：交易请求号

## 主键/索引
- PK：`party_order_no`
- FK：`wallet_order_no` → `t_wallet_order.wallet_order_no`

## 校验点(QA 关注)
- `wallet_order_no` 必须能在 `t_wallet_order` 中找到对应主单。
- 同一 `wallet_order_no` 下 party_order 条数应与主单 `party_count` 一致。
- `party_type` 取值应覆盖收/付方角色，且与主单 `order_type` 语义一致。
- `trade_amount` 与 `currency` 应与主单 `order_amount` / `currency` 在业务规则下对账一致。
- `partner_id` / `member_id` 与主单的对应字段需对齐（注意 party_order.partner_id 长度为 32，主单为 20，关注截断/不一致风险）。
- `status` 字段长度为 varchar/32，与主单 `status` (char/2) 编码体系不同，需确认状态机映射。
- `request_no` / `trade_request_no` 的幂等性与去重校验。

[[tbl_transferii_t_wallet_order]] [[wallet-redesign-send-money-er]]
