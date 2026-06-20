---
title: pix-RA-2405-STP-Wechat 微信支付时序流程
domain: remittance
kind: wiki_page
slug: pix-ra-2405-stp-wechat-flow
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:ef3f6539-9124-400a-b7f2-096dfe2a2761
tags: []
---

# pix-RA-2405-STP-Wechat 微信支付时序流程

本页描述 RA-2405 场景下，用户通过微信（Tenpay）完成扫码支付时，pix 作为编排核心与 wallet、cgs、tradeii 及 vendor(Tenpay) 之间的端到端交互时序。

## 参与方

- **User**：发起支付的用户
- **wallet**：钱包前端，负责收银台展示
- **cgs**：网关层
- **pix**：核心编排模块（本流程主导者）
- **tradeii**：交易记录服务
- **vendor(Tenpay)**：微信支付供应商

## 时序步骤

### 1. 确认交易信息
- **1** User → wallet：`confirm trade information`
- **1.1** wallet → cgs：调用 `/pix/mpc/v1/create-trade`
- **1.1.1** cgs → pix：同步转发请求

### 2. pix 编排下游调用
- **1.1.1.1** pix → vendor(Tenpay)：`scan code for payment`，向微信侧发起扫码支付
- **1.1.1.2** pix → tradeii：`CashierTradeFacade#createCashierTrade`，创建收银台交易记录
- **1.1.1.3** pix → cgs：返回结果（dashed return）

### 3. 收银台展示
- **1.2** cgs → wallet：返回结果
- **1.3** wallet → wallet：`show cashier`（自调用，渲染收银台 UI）
- **1.4** wallet → User：返回收银台界面

### 4. 用户完成支付
- **2** User → wallet：`complete cashier flow`，用户在收银台上完成后续支付动作

## 关键说明

- 实线箭头表示同步调用，虚线箭头表示返回。
- **pix** 为该流程的中心编排者：在收银台创建阶段，先向 Tenpay 发起扫码支付，再调用 tradeii 落库收银台交易，最后逐层返回至 wallet 渲染收银台。
- 创建收银台交易（`create-trade`）与用户完成收银台流程（`complete cashier flow`）属于两个独立步骤。
