---
title: ToC App充值下单时序流程
domain: payby-open-api
kind: wiki_page
slug: toc-add-funds-place-order-sequence
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:ef50c9db-622d-4c3c-8cd8-b8d2906636d5
tags: []
---

# ToC App充值下单时序流程

本页描述客户在 App 端发起充值（Add Funds）时，从 app-sdk 经 cgs 网关到下游服务的调用时序（Step 1: Place Order）。

## 参与角色

- **Customer**：客户（actor）
- **app-sdk**：App 端 SDK
- **cgs**：网关
- **personal**：个人账户域
- **deposit**：充值域
- **tradeii**：交易域
- **cashierii**：收银台域

## 调用时序

整体由两次经过 cgs 的调用组成：先 submit 创建充值订单并拿到 tokenUrl，再 init-trade 初始化交易。

### 1. submit deposit（创建充值订单）

1. `Customer → app-sdk`：submit deposit
2. `app-sdk → cgs`：`/personal/deposit/v1/auth/submit`
3. `cgs → personal`：转发调用
4. `personal → deposit`：`CashierDepositFacade#createCashierDeposit`
5. `deposit → tradeii`：`CashierTradeFacade#createCashierTrade`
6. `tradeii → cashierii`：`OrderTokenFacade#getTradeOrderToken`
7. `cashierii → tradeii`：返回 `cashierToken`
8. 逐层返回（tradeii → deposit → personal → cgs）
9. `cgs → app-sdk`：返回 `tokenUrl`

### 2. init-trade（初始化交易）

1. `app-sdk → cgs`：`/cashierii/order/v1/auth/init-trade`
2. `cgs → cashierii`：调用（跳过中间链路）
3. `cashierii → cgs`：返回
4. `cgs → app-sdk`：返回
5. `app-sdk → Customer`：返回

## 关键说明

- app-sdk 作为客户的前端入口，统一通过 cgs 网关访问后端服务，共发起两次网关调用。
- 第一次调用链路较深：`personal → deposit → tradeii → cashierii`，最终由 cashierii 颁发 `cashierToken`，向上层返回 `tokenUrl`。
- 第二次调用直接落在 cashierii，用于 init-trade 初始化交易。
