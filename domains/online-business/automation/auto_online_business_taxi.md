---
id: auto_online_business_taxi
object_type: AutomationAsset
name: 出租车支付自动化
aliases: [test_taxi_fangyong]
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-06-24'
source_type: repo
source_ref: cgs-apitest/testcases/payment/toB/test_taxi_fangyong.py
tags: [online-business, 支付, 自动化, cgs-apitest]
related_scenarios: [scn_online_business_cashier_pay]
related_services: [svc_cashierii, svc_acquireii, svc_tradeii, svc_payment, svc_member, svc_cards]
---

# 出租车支付自动化

> 来源 cgs-apitest 回归套件 `toB/test_taxi_fangyong.py`(4 TC)。覆盖场景 [[scn_online_business_cashier_pay]]。

## 用途
对「收银台支付 (Cashier / PayPage)」做端到端回归(pytest + allure)。

## 用例(TC)
| # | 用例 | 标题 |
| --- | --- | --- |
| 1 | `test_taxi_balancePay_payAmountLess` |  |
| 2 | `test_taxi_balancePay_payAmountMore` |  |
| 3 | `test_taxi_bindCard` |  |
| 4 | `test_taxi_bankCard` |  |

## 关联关系
- **覆盖的场景**:[[scn_online_business_cashier_pay]]
- **针对/跑在的服务**:[[svc_cashierii]]、[[svc_acquireii]]、[[svc_tradeii]]、[[svc_payment]]、[[svc_member]]、[[svc_cards]]

## 使用方式
- 入口:`pytest testcases/payment/toB/test_taxi_fangyong.py`;markers:`uat`/`sim`/`regression`。
- 依赖夹具:`get_env`/`get_urls`/`get_env_data`/`db_instance_factory`/`get_testdata`;业务封装 `CGSapi`/`SGS`/`Module`。

## 来源与置信
- cgs-apitest 仓 `toB/test_taxi_fangyong.py`;TC 列表来自源码(allure.title/函数名)。
