---
title: ToC Add Funds 充值时序流程
domain: payby-core-systems
kind: wiki_page
slug: toc-add-funds-flow
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:a0228e99-6349-44e8-8d89-3c6754fc7afa
tags: []
---

# ToC Add Funds 充值时序流程

本页描述 ToC 场景下用户发起 Add funds（充值）时，从客户端到收银台服务的端到端调用时序。完整流程概览见 [[flow_toc_add_funds]]。

## 参与方

- Customer（终端用户）
- app-sdk
- cgs
- personal
- deposit
- tradeii
- cashierii

## 主流程：提交充值并获取 tokenUrl

1. Customer → app-sdk：`submit deposit`
2. app-sdk → cgs：`/personal/deposit/v1/auth/submit`
3. cgs → personal：转发调用
4. personal → deposit：`CashierDepositFacade#createCashierDeposit`
5. deposit → tradeii：`CashierTradeFacade#createCashierTrade`
6. tradeii → cashierii：`OrderTokenFacade#getTradeOrderToken`
7. cashierii → tradeii：返回 `cashierToken`
8. 调用结果沿 tradeii → deposit → personal → cgs 逐层返回
9. cgs → app-sdk：返回 `tokenUrl`

## 后续流程：初始化交易（init-trade）

- app-sdk → cgs：`/cashierii/order/v1/auth/init-trade`
- cgs → cashierii：转发调用
- cashierii → cgs：返回结果
- cgs → app-sdk：返回结果
- app-sdk → Customer：返回最终响应

## 关键接口

| 调用方向 | 接口 |
|---|---|
| app-sdk → cgs | `/personal/deposit/v1/auth/submit` |
| personal → deposit | `CashierDepositFacade#createCashierDeposit` |
| deposit → tradeii | `CashierTradeFacade#createCashierTrade` |
| tradeii → cashierii | `OrderTokenFacade#getTradeOrderToken` |
| app-sdk → cgs | `/cashierii/order/v1/auth/init-trade` |

## 关键返回值

- `cashierToken`：由 cashierii 在 `getTradeOrderToken` 调用中返回给 tradeii
- `tokenUrl`：由 cgs 最终返回给 app-sdk，用于驱动后续 init-trade 流程
