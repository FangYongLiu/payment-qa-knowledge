---
id: flow_toc_add_funds
object_type: Flow
domain: fund-out-transfer
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-19'
source_type: wiki_image
source_ref: wiki_image:b7eefcfc-2e29-4ab9-96ba-c05fac6b4bfe
tags:
- add-funds
- bank-transfer
- cashier
subdomain: null
module: null
sensitivity: normal
name: ToC加款(银行转账)端到端流程
aliases: []
related_services:
- cgs
- personal
- fundout
- cashdesk-api
- app-sdk
related_tables: []
related_scenarios:
- toc-add-funds-flow
related_logs: []
related_requirements: []
related_failures: []
---

## 概述
ToC 加款(银行转账)端到端流程：Customer 通过 app-sdk 发起加款，经 cgs → personal → fundout 创建收银台收款单，并由 fundout 向 cashdesk-api 申请 fundout token，最终返回 cashierUrl 供 app-sdk 初始化收银台支付页。

## 步骤(跨系统)
1. Customer → app-sdk：发起加款流程
   - 1.1 app-sdk → cgs：`/personal/transfer/bank/submit`
     - 1.1.1 cgs → personal：(转发提交)
       - 1.1.1.1 personal → fundout：`CashierFundoutFacade#createCashierFundout`
         - 1.1.1.1.1 fundout → cashdesk-api：`TokenServiceFacade#getFundoutToken`
         - 1.1.1.1.2 cashdesk-api ⇠ fundout：返回 token
       - 1.1.1.2 fundout ⇠ personal：返回创建结果
     - 1.1.2 personal ⇠ cgs：返回
   - 1.2 cgs ⇠ app-sdk：返回 `cashierUrl`
   - 1.3 app-sdk → cashdesk-api：`/cashdesk/unityInitPayPage`
   - 1.4 cashdesk-api ⇠ app-sdk：返回收银台初始化结果
- 1.5 app-sdk ⇠ Customer：返回展示

## 涉及服务/表
- 服务：app-sdk、cgs、personal、fundout、cashdesk-api
- 关键接口：
  - cgs：`/personal/transfer/bank/submit`
  - fundout：`CashierFundoutFacade#createCashierFundout`
  - cashdesk-api：`TokenServiceFacade#getFundoutToken`、`/cashdesk/unityInitPayPage`

## 校验点
- `/personal/transfer/bank/submit` 提交链路是否串通至 fundout `createCashierFundout`
- fundout 是否成功通过 `TokenServiceFacade#getFundoutToken` 获取到 fundout token
- cgs 是否正确回传 `cashierUrl` 给 app-sdk
- app-sdk 是否成功调用 `/cashdesk/unityInitPayPage` 初始化收银台
