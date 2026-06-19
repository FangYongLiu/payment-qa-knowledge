---
title: ToC Add Funds 加款流程时序
domain: fund-out-transfer
kind: wiki_page
slug: toc-add-funds-flow
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:b7eefcfc-2e29-4ab9-96ba-c05fac6b4bfe
tags: []
---

# ToC Add Funds 加款流程时序

本页描述个人用户（ToC）通过银行转账方式发起加款（Add funds）的端到端调用链与各服务间的交互时序，归属业务域 `fund-out-transfer`。相关流程参见 [[flow_toc_add_funds]]。

## 参与方

时序图涉及以下角色与服务：

- **Customer**：发起加款的个人用户
- **app-sdk**：客户端 SDK
- **cgs**：网关服务
- **personal**：个人业务服务
- **fundout**：出款服务
- **cashdesk-api**：收银台 API 服务

## 调用时序

整体流程由 Customer 触发，经 app-sdk 提交至 cgs，再由 personal、fundout、cashdesk-api 协同完成，最终返回 `cashierUrl` 由客户端打开收银台页面。

### 1. 用户发起加款
- **1**：Customer → app-sdk，发起加款流程

### 2. 提交银行转账请求
- **1.1**：app-sdk → cgs，调用 `/personal/transfer/bank/submit`
- **1.1.1**：cgs → personal（内部调用）

### 3. 创建收银台出款单
- **1.1.1.1**：personal → fundout，调用 `CashierFundoutFacade#createCashierFundout`

### 4. 获取出款 Token
- **1.1.1.1.1**：fundout → cashdesk-api，调用 `TokenServiceFacade#getFundoutToken`
- **1.1.1.1.2**：cashdesk-api ⇠ fundout，返回 token

### 5. 逐层回传 cashierUrl
- **1.1.1.2**：fundout ⇠ personal，返回
- **1.1.2**：personal ⇠ cgs，返回
- **1.2**：cgs ⇠ app-sdk，返回 `cashierUrl`

### 6. 初始化收银台页面
- **1.3**：app-sdk → cashdesk-api，调用 `/cashdesk/unityInitPayPage`
- **1.4**：cashdesk-api ⇠ app-sdk，返回页面初始化结果
- **1.5**：app-sdk ⇠ Customer，向用户呈现收银台

## 关键接口与门面方法

| 调用环节 | 接口 / 方法 |
|---|---|
| 提交银行转账 | `/personal/transfer/bank/submit` |
| 创建收银台出款单 | `CashierFundoutFacade#createCashierFundout` |
| 获取出款 Token | `TokenServiceFacade#getFundoutToken` |
| 初始化收银台页面 | `/cashdesk/unityInitPayPage` |

## 流程要点

- 加款入口为银行转账提交接口 `/personal/transfer/bank/submit`，由 cgs 路由至 personal。
- personal 不直接对接收银台，而是通过 fundout 的 `CashierFundoutFacade` 创建收银台出款单。
- fundout 在创建过程中向 cashdesk-api 申请出款 token（`getFundoutToken`），用于收银台会话。
- 上游链路返回的 `cashierUrl` 由 app-sdk 用于后续 `unityInitPayPage` 初始化收银台页面，完成用户侧加款交互。
