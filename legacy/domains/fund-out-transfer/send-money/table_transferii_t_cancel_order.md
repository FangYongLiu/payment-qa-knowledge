---
id: tbl_transferii_t_cancel_order
object_type: Table
domain: fund-out-transfer
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-20'
source_type: wiki_image
source_ref: wiki_image:654d5bef-1e1a-485d-a44b-c83918b7165b
tags:
- transferii
- send-money
subdomain: send-money
module: null
sensitivity: normal
name: 取消订单表 t_cancel_order
aliases:
- Cancel Order
related_services: []
related_tables:
- tbl_transferii_t_wallet_order
- tbl_transferii_t_party_order
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
位于 `transferii` schema，用于记录 Send Money 场景下钱包订单的取消动作，与 `t_wallet_order`、`t_party_order` 配合形成订单生命周期数据模型。

## 关键列
- `cancel_order_no` — Cancel Order 编号(原文在该字段处截断，类型未给出)

> 注：原文图片在该表字段列表处截断，仅可见 `cancel_order_no` 一列；其余字段未在可见原文中出现。

## 主键/索引
- 主键：`cancel_order_no`(依据原文可见部分推断为该表的订单号字段；原文未显式标注 PK)

## 校验点(QA 关注)
- 取消记录应可关联到对应的 `t_wallet_order.wallet_order_no`，验证一笔钱包订单的取消链路完整。
- 与 `t_party_order` 的状态联动：取消发生时，相关参与方订单状态应同步流转。
- 原文未提供更多字段(如取消原因、操作人、时间戳、状态等)，QA 验证时需以实际 DDL 为准，不应基于本文档假设字段存在。
