---
id: auto_online_business_dynqr
object_type: AutomationAsset
name: 动态二维码收银自动化
aliases: [test_dynqr_fangyong]
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-06-24'
source_type: repo
source_ref: cgs-apitest/testcases/payment/toB/test_dynqr_fangyong.py
tags: [online-business, 支付, 自动化, cgs-apitest]
related_scenarios: [scn_online_business_cashier_pay]
related_services: [svc_cashierii, svc_acquireii, svc_tradeii, svc_payment, svc_member, svc_cards]
---

# 动态二维码收银自动化

> 来源 cgs-apitest 回归套件 `toB/test_dynqr_fangyong.py`(11 TC)。覆盖场景 [[scn_online_business_cashier_pay]]。

## 用途
对「收银台支付 (Cashier / PayPage)」做端到端回归(pytest + allure)。

## 用例(TC)
| # | 用例 | 标题 |
| --- | --- | --- |
| 1 | `test_dynqr_balance` |  |
| 2 | `test_dynqr_bindcard` |  |
| 3 | `test_dynqr_bankcard` |  |
| 4 | `test_dynqr_balance_refund` |  |
| 5 | `test_dynqr_bindcard_refund` |  |
| 6 | `test_dynqr_bindcard_NoKYC` |  |
| 7 | `test_dynqr_balance_cashierii` |  |
| 8 | `test_dynqr_bankcard_cashierii` |  |
| 9 | `test_dynqr_balance_simplifyCashierii` |  |
| 10 | `test_dynqr_bankcard_simplifyCashierii` |  |
| 11 | `test_dynqr_bindcard_NoKYC_simplifyCashierii` | N301：Simplified Cashier - NO KYC - Bind Card Payment |

## 关联关系
- **覆盖的场景**:[[scn_online_business_cashier_pay]]
- **针对/跑在的服务**:[[svc_cashierii]]、[[svc_acquireii]]、[[svc_tradeii]]、[[svc_payment]]、[[svc_member]]、[[svc_cards]]

## 使用方式
- 入口:`pytest testcases/payment/toB/test_dynqr_fangyong.py`;markers:`uat`/`sim`/`regression`。
- 依赖夹具:`get_env`/`get_urls`/`get_env_data`/`db_instance_factory`/`get_testdata`;业务封装 `CGSapi`/`SGS`/`Module`。

## 来源与置信
- cgs-apitest 仓 `toB/test_dynqr_fangyong.py`;TC 列表来自源码(allure.title/函数名)。
