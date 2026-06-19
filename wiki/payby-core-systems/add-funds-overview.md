---
title: Add Funds 充值业务总览
domain: payby-core-systems
kind: wiki_page
slug: add-funds-overview
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki
source_ref: wiki:30b14d13-f138-4933-9a9e-82e4ba95aaa6
tags: []
---

# Add Funds 充值业务总览

本页是 Add Funds（充值）业务在 payby-core-systems 域下的入口页，汇总目录、修订记录与文档说明性总览。

## 适用范围

- 业务域：payby-core-systems
- 业务主题：Add funds（充值）
- 子流程：[[add-funds-via-bank-card-flow]]（银行卡充值端到端流程，参见 [[flow_add_funds_via_bank_card]]）

## 目录

1. Table of contents
2. Revision
3. Purpose
4. Add funds via Bank Card

## 修订记录 (Revision)

| Date | Content | Revisor |
|---|---|---|
| 20 Oct 2025 | Add funds via Bank Card；BOTIM Transfer；Withdraw via IBAN | Cong Zhou |
| 23 Mar 2026 | Move BOTIM transfer to ToC - Transfer 页面 | Cong Zhou |

## 文档目的 (Purpose)

本系列文档遵循以下编写约定：

- 仅描述主流程的系统调用链路。
- 为聚焦支付系统核心架构，省略以下查询/辅助操作：
  - member、merchant 查询
  - 费用计算 (fee calculation)
  - 结算周期 (settlement cycle)
  - 商户支付方式鉴权查询 (merchant payment method authentication queries)
  - 风控识别 (risk control identify)
  - 渠道路由 (channel routing)
- 在新系统设计图中，**不建议**纳入此类间接依赖系统。

## 包含的子流程

- **Add funds via Bank Card** — 银行卡充值，详见 [[add-funds-via-bank-card-flow]]。该流程拆分为：
  - Step 1: Place Order（下单）
  - Step 2: Card Pay（卡支付，含 3DS 验证与支付结果回调）

> 说明：BOTIM Transfer 已迁移至 ToC - Transfer 文档；Withdraw via IBAN 属于提现域，不在本页 scope。
