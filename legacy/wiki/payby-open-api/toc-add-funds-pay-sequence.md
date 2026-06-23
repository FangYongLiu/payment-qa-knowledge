---
title: ToC Add Funds 支付时序流程
domain: payby-open-api
kind: wiki_page
slug: toc-add-funds-pay-sequence
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:6a1293b5-35f9-4891-b282-215f2db62f85
tags: []
---

# ToC Add Funds 支付时序流程

本页描述 ToC 场景下 Add Funds（充值）支付环节（Step 2: Pay）从 App 端提交到银行 3DS 验证的端到端调用时序。

## 参与方（Lifelines）

按时序图从左到右：

- Customer（用户）
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

## 主流程时序

### 1. Customer 提交充值

- `1` Customer → app-sdk：submit deposit

### 1.1 确认支付（confirm-pay）

- `1.1` app-sdk → cgs：`/cashierii/pay/v1/auth/confirm-pay`
- `1.1.1` cgs → cashierii
- `1.1.1.1` cashierii → grc-component-connect-provider：`PaymentSessionQueryStub#paymentSessionQuery`

### 1.2 校验并发起支付（verify）

- `1.2` app-sdk → cgs：`/cashierii/pay/v1/auth/verify`
- `1.2.1` cgs → cashierii
- `1.2.1.1` cashierii → cmf：`CardTokenFacade#create`
- `1.2.1.2` cashierii → tradeii：`CashierTradePayFacade#confirmPay`
  - `1.2.1.2.1` tradeii → pfs-payment：`QuickPayPaymentFacade#pay`
    - `1.2.1.2.1.1` pfs-payment → payment：`PaymentFacade#pay`
      - `1.2.1.2.1.1.1` payment → cmf：`FundRequestFacade#apply`
        - `1.2.1.2.1.1.1.1` cmf → qpay-cko：`ChannelFundFacade#apply`
          - `1.2.1.2.1.1.1.1.1` qpay-cko → fcw

### 1.3 返回 3DS 表单

- `1.3` app-sdk ⇢ Customer（虚线返回）：3ds bank form

## 2. 3DS 银行验证

- `2` Customer → BANK：request and complete 3ds verify

## 关键调用链一览

- 入口接口：`/cashierii/pay/v1/auth/confirm-pay` → `/cashierii/pay/v1/auth/verify`
- 核心 Facade 调用顺序：
  1. `PaymentSessionQueryStub#paymentSessionQuery`（会话查询）
  2. `CardTokenFacade#create`（卡 Token 创建）
  3. `CashierTradePayFacade#confirmPay`（收银台支付确认）
  4. `QuickPayPaymentFacade#pay`（快捷支付）
  5. `PaymentFacade#pay`（支付）
  6. `FundRequestFacade#apply`（资金申请）
  7. `ChannelFundFacade#apply`（渠道资金申请）
- 渠道侧出口：qpay-cko → fcw → BANK（完成 3DS）
