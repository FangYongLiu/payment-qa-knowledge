---
title: Wallet Redesign Send Money 数据模型
domain: fund-out-transfer
kind: wiki_page
slug: wallet-redesign-send-money-er
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:654d5bef-1e1a-485d-a44b-c83918b7165b
tags: []
---

# Wallet Redesign Send Money 数据模型

本页梳理 Send Money 功能在 `transferii` schema 下的核心表结构与表间关系，覆盖钱包订单、参与方订单、收款凭证及取消订单四张主表。

## Schema 总览

- 数据库 schema：`transferii`
- 业务域：`fund-out-transfer`（Send Money）
- 主要表：
  - `t_wallet_order`：钱包订单主表
  - `t_party_order`：参与方订单表
  - `t_order_permit`：订单收款凭证表（Collect Permit）
  - `t_cancel_order`：取消订单表

## 表间关系

- `t_wallet_order.wallet_order_no` 为主键，是整个 Send Money 数据模型的核心。
- `t_party_order.wallet_order_no`（FK）→ `t_wallet_order.wallet_order_no`，一个钱包订单对应多个参与方订单（party_count 记录数量）。
- `t_order_permit.wallet_order_no`（FK）→ `t_wallet_order.wallet_order_no`，关联收款凭证。
- `t_cancel_order` 关联到钱包订单，用于记录取消动作。

## 核心表速览

### 钱包订单主表 [[tbl_transferii_t_wallet_order]]
- 主键：`wallet_order_no` (varchar/32)
- 关键字段：`order_type`、`partner_id`、`member_id`、`order_amount` (decimal 19,4)、`party_count`、`currency`、`status`、`expire_time`、`trade_extension`

### 参与方订单表 [[tbl_transferii_t_party_order]]
- 主键：`party_order_no` (bigint)
- 外键：`wallet_order_no` → t_wallet_order
- 关键字段：`request_no`、`partner_id`、`member_id`、`party_type`、`trade_amount`、`currency`、`status`、`trade_request_no`

### 订单收款凭证表 [[tbl_transferii_t_order_permit]]
- 主键：`permit_id` (bigint)
- 外键：`wallet_order_no` → t_wallet_order
- 关键字段：`permit_type` (char/1)、`permit_value` (varchar/32)

### 取消订单表 [[tbl_transferii_t_cancel_order]]
- 主键：`cancel_order_no`
- 用途：记录针对钱包订单的取消操作（原文未给出完整字段列表）
