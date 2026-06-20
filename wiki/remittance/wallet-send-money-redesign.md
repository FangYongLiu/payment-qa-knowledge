---
title: Wallet Redesign - Send Money 需求说明
domain: remittance
kind: wiki_page
slug: wallet-send-money-redesign
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki
source_ref: wiki:77b3f2a6-a8a3-4481-944a-58fb9f23fdda
tags: []
---

# Wallet Redesign - Send Money 需求说明

本页梳理 Wallet Redesign 项目中 Send Money 功能的整体需求，包括与既有手机号转账方式的差异、典型用户场景以及发送、领取、KYC、订单过期等关键功能点。

## 资料入口

- 需求文档：Send
- UI 设计稿：Figma - Local Transfer

## 与手机号转账的核心差异

详见 [[send-money-vs-phone-transfer]]，主要差异聚焦于资金流、领取方式、退款规则与通知渠道：

- **付款资金流**
  - 手机号转账：付款人 → 付款人中间户 → 收款人（无论收款人是否 KYC）
  - Send Money（收款人已 KYC）：付款人自动结算 → 收款人
  - Send Money（收款人未 KYC）：付款人手动结算 → 收款人
- **领取方式**
  - 手机号转账（已 KYC）：通知付款成功后调用 transfer 结算，存在失败可能
  - 手机号转账（未 KYC）：公众号通知，KYC 后用户手动领取
  - Send Money（已 KYC）：付款时直接自动结算
  - Send Money（未 KYC）：聊天气泡通知，KYC 后系统自动结算（仍可能失败）
- **退款规则**
  - 手机号转账（未 KYC）：24H 退款 + 公众号通知
  - Send Money（未 KYC）：72H 退款 + 聊天气泡通知
  - 已 KYC 场景：手机号转账自动领取失败 24H 退款；Send Money 仅出现支付失败
- **通知渠道（自动结算成功）**
  - 手机号转账：付款方公众号通知；收款方短信 + 公众号通知
  - Send Money：付款方转账成功聊天气泡；收款方到账聊天气泡

## User Cases

覆盖发送方与接收方在不同 KYC 状态、不同领取/过期路径下的组合场景（详见原文用例图）。端到端流程参见 [[flow_send_money]]。

## 需求功能点

### 5.1 发送转账

定义付款人发起 Send Money 的交互与状态流转（详见原文流程图）。

### 5.2 发送和领取

描述付款成功后的领取分支：

- 收款人已 KYC：自动结算到账
- 收款人未 KYC：进入待领取状态，等待 KYC 后系统自动领取

### 5.3 收款人完成 KYC

收款人在转账存续期内完成 KYC 后，系统触发自动结算并通知双方；自动结算仍存在失败可能。

### 5.4 订单过期

未 KYC 收款人未在有效期内完成 KYC 时，订单过期并按 72H 规则触发退款，通过聊天气泡通知付款方。

## 数据库设计

包含 Send Money 订单、领取状态、退款记录等相关表（详见原文 ER 图）。
