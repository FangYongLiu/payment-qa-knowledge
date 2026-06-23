---
title: ToC Withdraw Add Funds 时序流程
domain: withdraw-cash
kind: wiki_page
slug: toc-withdraw-add-funds-sequence
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:17f821b7-3635-4056-93f2-22798ef4b598
tags: []
---

# ToC Withdraw Add Funds 时序流程

本页梳理 ToC 场景下客户通过银行转账充值（Add funds）时，从客户端到各后端服务的调用时序，以及收银台 URL 的生成与初始化链路。完整业务流程见 [[flow_toc_withdraw_add_funds]]。

## 参与方

- Customer：终端客户
- app-sdk：客户端 SDK
- cgs：网关服务
- personal：个人账户服务
- fundout：出款服务
- cashdesk-api：收银台 API 服务

## 调用时序

按编号顺序描述各服务间的调用与返回。

### 1. 客户发起充值
- `1` Customer → app-sdk：用户在客户端触发 Add funds。

### 1.1 提交银行转账
- `1.1` app-sdk → cgs：`/personal/transfer/bank/submit`
- `1.1.1` cgs → personal：转发请求至个人账户服务

### 1.1.1.1 创建收银台出款单
- `1.1.1.1` personal → fundout：`CashierFundoutFacade#createCashierFundout`

### 1.1.1.1.1 获取 Fundout Token
- `1.1.1.1.1` fundout → cashdesk-api：`TokenServiceFacade#getFundoutToken`
- `1.1.1.1.2` cashdesk-api ⇠ fundout：返回 token

### 返回链路（生成 cashierUrl）
- `1.1.1.2` fundout ⇠ personal：返回结果
- `1.1.2` personal ⇠ cgs：返回结果
- `1.2` cgs ⇠ app-sdk：返回 `cashierUrl`

### 1.3 初始化收银台页面
- `1.3` app-sdk → cashdesk-api：`/cashdesk/unityInitPayPage`
- `1.4` cashdesk-api ⇠ app-sdk：返回页面初始化结果

### 1.5 返回客户
- `1.5` app-sdk ⇠ Customer：完成充值收银台展示

## 关键链路要点

- 收银台 URL 的源头：由 `fundout` 调用 `cashdesk-api` 的 `TokenServiceFacade#getFundoutToken` 获取 token，逐层向上返回，最终由 `cgs` 以 `cashierUrl` 形式回传给 `app-sdk`。
- 出款单创建入口：`personal` 通过 `CashierFundoutFacade#createCashierFundout` 委派给 `fundout`。
- 客户端两次访问 `cashdesk-api`：一次间接（经 fundout 取 token）、一次直接（`/cashdesk/unityInitPayPage` 初始化收银台页面）。
