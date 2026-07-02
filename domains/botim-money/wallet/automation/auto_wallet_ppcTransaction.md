---
id: auto_wallet_ppcTransaction
object_type: AutomationAsset
name: PPC 交易自动化
aliases: [test_ppcTransaction_jianfei]
domain: wallet
status: active
owner: qianlong.wang
reviewer: qianlong.wang
last_reviewed_at: '2026-06-24'
source_type: repo
source_ref: cgs-apitest/testcases/payment/toC/test_ppcTransaction_jianfei.py
tags: [wallet, 支付, 自动化, cgs-apitest]
related_scenarios: [scn_wallet_consumer_pay]
related_services: [svc_tradeii, svc_payment, svc_member, svc_cashierii]
---

# PPC 交易自动化

> 来源 cgs-apitest 回归套件 `toC/test_ppcTransaction_jianfei.py`(45 TC)。覆盖场景 [[scn_wallet_consumer_pay]]。

## 用途
对「消费者付款 (Payment Code / PPC)」做端到端回归(pytest + allure)。

## 用例(TC)
| # | 用例 | 标题 |
| --- | --- | --- |
| 1 | `test_ppcAuth_PosPurchase` |  |
| 2 | `test_ppcAuth_PosPurchaseReversal` |  |
| 3 | `test_ppcAuth_PosPurchaseRelease` |  |
| 4 | `test_ppcAuth_PosPurchaseSettle` |  |
| 5 | `test_ppcAuth_ATMWithdrawl` |  |
| 6 | `test_ppcAuth_ATMWithdrawlReversal` |  |
| 7 | `test_ppcAuth_ATMWithdrawlRelease` |  |
| 8 | `test_ppcAuth_ATMWithdrawlSettle` |  |
| 9 | `test_ppcAuth_PreAuth` |  |
| 10 | `test_ppcAuth_PreAuthReversal` |  |
| 11 | `test_ppcAuth_PreAuthRelease` |  |
| 12 | `test_ppcAuth_PreAuthSettle` |  |
| 13 | `test_ppcAuth_PreAuthCompletion` |  |
| 14 | `test_ppcAuth_PreAuthCompletionReversal` |  |
| 15 | `test_ppcAuth_PreAuthCompletionRelease` |  |
| 16 | `test_ppcAuth_PreAuthCompletionSettle` |  |
| 17 | `test_ppcAuth_Refund` |  |
| 18 | `test_ppcAuth_Refund_Reversal` |  |
| 19 | `test_ppcAuth_PosPurchase_Settle` |  |
| 20 | `test_ppcAuth_Offline_Settle` |  |
| 21 | `test_ppcAuth_BalanceEnquiryFee` |  |
| 22 | `test_ppcAuth_ATMDecline` |  |
| 23 | `test_ppcAuth_ReversaOfPosPurchaseSettle` |  |
| 24 | `test_ppcAuth_ReversaOfATMWithdrawalSettle` |  |
| 25 | `test_ppcAuth_ReversalofPosPurchaseSettle` |  |
| 26 | `test_ppcAuth_ReversalOfOfflineSettle` |  |
| 27 | `test_ppcAuth_ReversalOfSettle` |  |
| 28 | `test_ppcAuth_Charegback` |  |
| 29 | `test_ppcAuth_masterCardSend` |  |
| 30 | `test_ppcAuth_masterCardSend_kyc` |  |
| 31 | `test_ppcAuth_masterCardSend` |  |
| 32 | `test_ppcAuth_masterCardSend_limit` |  |
| 33 | `test_ppcAuth_reversalMasterCardSend` |  |
| 34 | `test_ppcAuth_PartialReversalPurchase` |  |
| 35 | `test_ppcAuth_E400` |  |
| 36 | `test_ppcAuth_E401` |  |
| 37 | `test_ppcAuth_E402` |  |
| 38 | `test_ppcAuth_E200` |  |
| 39 | `test_ppcAuth_E201` |  |
| 40 | `test_ppcAuth_E202` |  |
| 41 | `test_ppcAuth_E203` |  |
| 42 | `test_ppcAuth_E204` |  |
| 43 | `test_ppcAuth_E205` |  |
| 44 | `test_ppcAuth_E206` |  |
| 45 | `test_ppcAuth_E207` |  |

## 关联关系
- **覆盖的场景**:[[scn_wallet_consumer_pay]]
- **针对/跑在的服务**:[[svc_tradeii]]、[[svc_payment]]、[[svc_member]]、[[svc_cashierii]]

## 使用方式
- 入口:`pytest testcases/payment/toC/test_ppcTransaction_jianfei.py`;markers:`uat`/`sim`/`regression`。
- 依赖夹具:`get_env`/`get_urls`/`get_env_data`/`db_instance_factory`/`get_testdata`;业务封装 `CGSapi`/`SGS`/`Module`。

## 来源与置信
- cgs-apitest 仓 `toC/test_ppcTransaction_jianfei.py`;TC 列表来自源码(allure.title/函数名)。
