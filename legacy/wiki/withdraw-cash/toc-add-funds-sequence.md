---
title: ToC Add Funds 充值时序流程
domain: withdraw-cash
kind: wiki_page
slug: toc-add-funds-sequence
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:41b21404-f935-45de-b932-358f4a10bb5d
tags: []
---

# ToC Add Funds 充值时序流程

本页描述 ToC Add funds 场景下，从 Customer 提交转账到 cashierii 初始化交易的端到端服务调用时序。

## 参与方

- Customer（终端用户）
- app-sdk
- cgs
- personal
- transfer
- tradeii
- cashierii

## 主流程：提交转账并获取 tokenUrl

1. Customer → app-sdk：`submit transfer`
2. app-sdk → cgs：`/personal/transfer/submit`
3. cgs → personal（转发）
4. personal → transfer：`TransferOrderFacade#recruitTransfer`
5. transfer → tradeii：`CashierTradeFacade#createCashierTrade`
6. tradeii → cashierii：`OrderTokenFacade#getTradeOrderToken`
7. cashierii 返回 `cashierToken` 给 tradeii
8. 调用结果沿 tradeii → transfer → personal → cgs 逐层返回
9. cgs 向 app-sdk 返回 `tokenUrl`

## 后续：初始化交易

1. app-sdk → cgs：`/cashierii/order/v1/auth/init-trade`
2. cgs → cashierii（直接调用，跳过 personal / transfer / tradeii）
3. cashierii 返回结果给 cgs

## 关键接口与返回值

- 提交转账入口：`/personal/transfer/submit`
- 初始化交易入口：`/cashierii/order/v1/auth/init-trade`
- 内部 Facade 调用链：
  - `TransferOrderFacade#recruitTransfer`
  - `CashierTradeFacade#createCashierTrade`
  - `OrderTokenFacade#getTradeOrderToken`
- 关键返回字段：`cashierToken`、`tokenUrl`

## 调用链特征

- 第一段（submit transfer）逐层下穿四层服务（personal → transfer → tradeii → cashierii）以生成 `cashierToken`，最终聚合为 `tokenUrl` 返回给 app-sdk。
- 第二段（init-trade）由 cgs 直连 cashierii，不经过 personal / transfer / tradeii。
