---
id: auto_online_business_auto_debit
object_type: AutomationAsset
name: 自动代扣自动化
aliases: [test_auto_debit_fangyong]
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-06-24'
source_type: repo
source_ref: cgs-apitest/testcases/payment/toB/test_auto_debit_fangyong.py
tags: [online-business, 支付, 自动化, cgs-apitest]
related_scenarios: [scn_online_business_auto_debit]
related_services: [svc_authpay, svc_deduct, svc_tradeii, svc_payment, svc_member, svc_cards]
---

# 自动代扣自动化

> 来源 cgs-apitest 回归套件 `toB/test_auto_debit_fangyong.py`(7 TC)。覆盖场景 [[scn_online_business_auto_debit]]。

## 用途
对「自动代扣 / 签约 (Auto Debit)」做端到端回归(pytest + allure)。

## 用例(TC)
| # | 用例 | 标题 |
| --- | --- | --- |
| 1 | `test_autodebit_balance` | N101:Autodebit pay with balance |
| 2 | `test_autodebit_bankcard` | N102:Autodebit pay with bankcard |
| 3 | `test_autodebit_balanceAndBankcard` | N103:Autodebit pay with balance and bankcard |
| 4 | `test_autodebit_balanceAndBankcardPayFail` | N104:Autodebit pay with balance and bankcard pay fail |
| 5 | `test_autodebit_BankcardPayFail` | N105:Autodebit pay with balance and bankcard pay fail |
| 6 | `test_autodebit_balance_refund` | N106:Autodebit pay with balance then refund |
| 7 | `test_autodebit_bankcard_refund` | N107:Autodebit pay with bankcard |

## 关联关系
- **覆盖的场景**:[[scn_online_business_auto_debit]]
- **针对/跑在的服务**:[[svc_authpay]]、[[svc_deduct]]、[[svc_tradeii]]、[[svc_payment]]、[[svc_member]]、[[svc_cards]]

## 使用方式
- 入口:`pytest testcases/payment/toB/test_auto_debit_fangyong.py`;markers:`uat`/`sim`/`regression`。
- 依赖夹具:`get_env`/`get_urls`/`get_env_data`/`db_instance_factory`/`get_testdata`;业务封装 `CGSapi`/`SGS`/`Module`。

## 来源与置信
- cgs-apitest 仓 `toB/test_auto_debit_fangyong.py`;TC 列表来自源码(allure.title/函数名)。
