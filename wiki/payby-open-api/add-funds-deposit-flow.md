---
title: Add Funds 充值交易时序流程
domain: payby-open-api
kind: wiki_page
slug: add-funds-deposit-flow
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:5d857d21-abfb-434d-a195-7f7a84e5418b
tags: []
---

# Add Funds 充值交易时序流程

本页描述客户从 app-sdk 发起充值，到银行完成 3DS 验证的端到端调用链与各参与服务的交互顺序。

## 参与方

按时序图泳道从左至右：

- Customer（客户）
- app-sdk
- cgs
- cashierii
- grc-component-connect-provider
- deposit
- tradeii
- pfs-payment
- payment
- cmf
- qpay-cko
- fcw
- BANK

## 调用时序

### 1. 提交充值

- **1** Customer → app-sdk：submit deposit

### 1.1 确认支付（confirm-pay）

- **1.1** app-sdk → cgs：`/cashierii/pay/v1/auth/confirm-pay`
- **1.1.1** cgs → cashierii
- **1.1.1.1** cashierii → grc-component-connect-provider：`PaymentSessionQueryStub#paymentSessionQuery`

### 1.2 校验与扣款链路（verify）

- **1.2** app-sdk → cgs：`/cashierii/pay/v1/auth/verify`
- **1.2.1** cgs → cashierii
- **1.2.1.1** cashierii → cmf：`CardTokenFacade#create`
- **1.2.1.2** cashierii → tradeii：`CashierTradePayFacade#confirmPay`
  - **1.2.1.2.1** tradeii → pfs-payment：`QuickPayPaymentFacade#pay`
    - **1.2.1.2.1.1** pfs-payment → payment：`PaymentFacade#pay`
      - **1.2.1.2.1.1.1** payment → cmf：`FundRequestFacade#apply`
        - **1.2.1.2.1.1.1.1** cmf → qpay-cko：`ChannelFundFacade#apply`
          - **1.2.1.2.1.1.1.1.1** qpay-cko → fcw

### 1.3 返回 3DS 表单

- **1.3** app-sdk ⇠ Customer：返回 `3ds bank form`

### 2. 银行 3DS 验证

- **2** Customer → BANK：request and complete 3ds verify
- **3** BANK：（后续银行回执处理）

## 关联流程

- 端到端业务视角参见 [[flow_add_funds_deposit]]。
