---
id: flow_toc_add_funds
object_type: Flow
domain: payby-core-systems
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-19'
source_type: wiki_image
source_ref: wiki_image:a0228e99-6349-44e8-8d89-3c6754fc7afa
tags:
- ToC
- AddFunds
- Deposit
- Cashier
subdomain: null
module: null
sensitivity: normal
name: ToC Add Funds 充值端到端流程
aliases: []
related_services: []
related_tables: []
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 概述
ToC Add Funds（充值）端到端流程：Customer 通过 app-sdk 发起充值，经 cgs 网关路由到 personal，依次调用 deposit 创建充值单、tradeii 创建交易单，并由 cashierii 生成 cashierToken 返回 tokenUrl；随后 app-sdk 再次通过 cgs 调用 cashierii 初始化交易（init-trade）。

## 步骤(跨系统)
1. Customer → app-sdk: `submit deposit`
   1.1 app-sdk → cgs: `POST /personal/deposit/v1/auth/submit`
       1.1.1 cgs → personal: 调用充值提交逻辑
            1.1.1.1 personal → deposit: `CashierDepositFacade#createCashierDeposit`
                 1.1.1.1.1 deposit → tradeii: `CashierTradeFacade#createCashierTrade`
                      1.1.1.1.1.1 tradeii → cashierii: `OrderTokenFacade#getTradeOrderToken`
                      1.1.1.1.1.2 cashierii → tradeii: 返回 `cashierToken`
                 1.1.1.1.2 tradeii → deposit: 返回
            1.1.1.2 deposit → personal: 返回
       1.1.2 personal → cgs: 返回
   1.2 cgs → app-sdk: 返回 `tokenUrl`
2. 第二次往返：初始化收银台交易
   1.3 app-sdk → cgs: `POST /cashierii/order/v1/auth/init-trade`
       1.3.1 cgs → cashierii: 调用 init-trade
       1.3.2 cashierii → cgs: 返回
   1.4 cgs → app-sdk: 返回
   1.5 app-sdk → Customer: 返回

## 涉及服务/表
- 服务：app-sdk、cgs、personal、deposit、tradeii、cashierii
- 关键 Facade/接口：
  - `CashierDepositFacade#createCashierDeposit` (personal → deposit)
  - `CashierTradeFacade#createCashierTrade` (deposit → tradeii)
  - `OrderTokenFacade#getTradeOrderToken` (tradeii → cashierii)
- 关键 HTTP 路径：
  - `/personal/deposit/v1/auth/submit`
  - `/cashierii/order/v1/auth/init-trade`

## 校验点
- 第一阶段 submit 链路返回 `tokenUrl`（由 cashierii 生成的 `cashierToken` 透传至 app-sdk）。
- 第二阶段 app-sdk 必须使用 token 通过 cgs 调用 `init-trade` 完成交易初始化。
- cgs 在 init-trade 调用中直接路由到 cashierii，跳过中间 personal/deposit/tradeii 链路。
