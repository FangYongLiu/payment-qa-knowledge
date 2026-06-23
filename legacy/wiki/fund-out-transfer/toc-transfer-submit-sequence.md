---
title: ToC转账提交时序流程
domain: fund-out-transfer
kind: wiki_page
slug: toc-transfer-submit-sequence
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:319ed6b1-9d7d-451d-ae3c-f9e347913848
tags: []
---

# ToC转账提交时序流程

本页描述 C 端用户提交转账时，从 `app-sdk` 到 `cgs`、`personal`、`transfer`、`tradeii`、`cashierii` 的调用链路，以及最终返回 `tokenUrl` 并发起 init-trade 的过程。

## 参与方

- Customer（C 端用户）
- app-sdk
- cgs
- personal
- transfer
- tradeii
- cashierii

## 调用时序

1. Customer → app-sdk：`submit transfer`
2. app-sdk → cgs：`/personal/transfer/submit`
3. cgs → personal
4. personal → transfer：`TransferOrderFacade#recruitTransfer`
5. transfer → tradeii：`CashierTradeFacade#createCashierTrade`
6. tradeii → cashierii：`OrderTokenFacade#getTradeOrderToken`
7. cashierii 返回 `cashierToken` 给 tradeii
8. tradeii、transfer、personal 依次原路返回至 cgs
9. cgs 返回 `tokenUrl` 给 app-sdk

## 后续 init-trade 调用

获得 `tokenUrl` 后，app-sdk 继续发起鉴权初始化交易：

- app-sdk → cgs：`/cashierii/order/v1/auth/init-trade`
- cgs → cashierii（直接调用，跳过 personal / transfer / tradeii）
- cashierii 返回结果给 cgs

## 关键说明

- 提交阶段（submit）链路较长：`cgs → personal → transfer → tradeii → cashierii`，由 cashierii 通过 `OrderTokenFacade#getTradeOrderToken` 生成 `cashierToken`，逐层回传，最终在 cgs 层组装成 `tokenUrl` 返回 app-sdk。
- init-trade 阶段链路被简化：cgs 直接调用 cashierii，不再经过 personal、transfer、tradeii。
