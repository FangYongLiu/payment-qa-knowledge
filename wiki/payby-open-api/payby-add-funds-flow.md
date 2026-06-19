---
title: PayBy Add Funds 充值时序流程
domain: payby-open-api
kind: wiki_page
slug: payby-add-funds-flow
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:b67afc99-27cc-4620-b601-f4b4f72c21d4
tags: []
---

# PayBy Add Funds 充值时序流程

本页描述 Customer 发起充值（Add funds / deposit）后，从 app-sdk 经 cgs、personal、deposit、tradeii 到 cashierii 的完整调用时序与关键接口。

## 参与方（Lifelines）

- Customer（终端用户）
- app-sdk
- cgs
- personal
- deposit
- tradeii
- cashierii

## 调用时序

按编号顺序列出消息（同步调用使用实线，返回值使用虚线）。

### 1. 提交充值并获取 tokenUrl

- **1**: `submit deposit` — Customer → app-sdk
- **1.1**: `/personal/deposit/v1/auth/submit` — app-sdk → cgs
  - **1.1.1**: cgs → personal
    - **1.1.1.1**: `CashierDepositFacade#createCashierDeposit` — personal → deposit
      - **1.1.1.1.1**: `CashierTradeFacade#createCashierTrade` — deposit → tradeii
        - **1.1.1.1.1.1**: `OrderTokenFacade#getTradeOrderToken` — tradeii → cashierii
        - **1.1.1.1.1.2**: `cashierToken`（返回） — cashierii ⇠ tradeii
      - **1.1.1.1.2**: 返回 — tradeii ⇠ deposit
    - **1.1.1.2**: 返回 — deposit ⇠ personal
  - **1.1.2**: 返回 — personal ⇠ cgs
- **1.2**: `tokenUrl`（返回） — cgs ⇠ app-sdk

### 2. 初始化收银台交易

- **1.3**: `/cashierii/order/v1/auth/init-trade` — app-sdk → cgs
  - **1.3.1**: cgs → cashierii
  - **1.3.2**: 返回 — cashierii ⇠ cgs
- **1.4**: 返回 — cgs ⇠ app-sdk
- **1.5**: 返回 — app-sdk ⇠ Customer

## 关键接口与方法

- HTTP 接口（cgs 暴露给 app-sdk）：
  - `/personal/deposit/v1/auth/submit`：提交充值，返回 `tokenUrl`
  - `/cashierii/order/v1/auth/init-trade`：初始化收银台交易
- 内部 Facade 调用：
  - `CashierDepositFacade#createCashierDeposit`（personal → deposit）
  - `CashierTradeFacade#createCashierTrade`（deposit → tradeii）
  - `OrderTokenFacade#getTradeOrderToken`（tradeii → cashierii），返回 `cashierToken`

## 流程要点

- 整个充值由两次客户端→cgs 的请求驱动：先 `submit` 拿到 `tokenUrl`，再 `init-trade` 启动收银台交易。
- 服务链路按 personal → deposit → tradeii → cashierii 逐层下钻，最深处由 cashierii 生成 `cashierToken`，逐层回传后由 cgs 组装为 `tokenUrl` 返回 app-sdk。
- 业务域：`payby-open-api`。
