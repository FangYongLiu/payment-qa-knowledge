---
title: Send Money需求功能点
domain: remittance
kind: wiki_page
slug: send-money-feature-requirements
status: archived
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:PMDPayment/185794690
tags: []
---

# Send Money需求功能点

本页梳理 Send Money 业务在转账核心链路上的功能需求范围，涵盖发送转账、发送与领取、收款人 KYC 完成后的处理、以及订单过期四个主题。与手机号转账的差异对比见 [[send-money-vs-phone-transfer]]，端到端流程见 [[flow_send_money]]。

## 功能范围概览

Send Money 的需求功能点划分为四个子场景：

- 发送转账
- 发送和领取
- 收款人完成 KYC
- 订单过期

每个子场景均有对应的交互与流程图（详见原始 Figma 与 PRD）。

## 发送转账

聚焦付款人发起 Send Money 转账的核心动作，包括：

- 付款人选择收款人并发起转账
- 根据收款人 KYC 状态决定资金流走向
  - 收款人已 KYC：付款人 → 收款人，自动结算
  - 收款人未 KYC：付款人 → 收款人，手动结算（待领取）
- 付款方收到转账成功的聊天气泡通知

## 发送和领取

描述转账发出后的领取链路：

- 收款人已 KYC 场景下：付款直接自动结算给收款人，收款方收到转账到账聊天气泡通知
- 收款人未 KYC 场景下：
  - 通过聊天气泡通知收款人有转账待领取
  - 收款人完成 KYC 前，款项处于待领取状态
- 自动领取存在失败可能，失败时进入退款链路（已 KYC 场景下 24H 退款）

## 收款人完成 KYC

针对未 KYC 收款人在转账后完成 KYC 的处理：

- 收款人完成 KYC 后，系统自动结算领取
- 自动结算仍存在失败可能性
- 自动结算成功后，按 Send Money 通知规则发送聊天气泡通知

## 订单过期

针对未及时领取的转账订单的过期与退款处理：

- 收款人未 KYC：72H 后退款，并发送聊天气泡通知
- 收款人已 KYC：仅在自动领取失败时走 24H 退款，不存在长时间未领取过期场景（仅可能出现支付失败）

## 数据库设计

需求附带数据库设计图，定义 Send Money 订单、领取状态、退款等相关表结构（详见原文设计图）。
