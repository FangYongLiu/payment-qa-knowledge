---
id: auto_online_business_smart_pos
object_type: AutomationAsset
name: 智能 POS 自动化
aliases: [test_smart_pos]
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-06-24'
source_type: repo
source_ref: cgs-apitest/testcases/payment/toB/test_smart_pos.py
tags: [online-business, 支付, 自动化, cgs-apitest]
related_scenarios: [scn_online_business_cashier_pay]
related_services: [svc_cashierii, svc_acquireii, svc_tradeii, svc_payment, svc_member, svc_cards]
---

# 智能 POS 自动化

> 来源 cgs-apitest 回归套件 `toB/test_smart_pos.py`(3 TC)。覆盖场景 [[scn_online_business_cashier_pay]]。

## 用途
对「收银台支付 (Cashier / PayPage)」做端到端回归(pytest + allure)。

## 用例(TC)
| # | 用例 | 标题 |
| --- | --- | --- |
| 1 | `test_SmartPos_placeOder` |  |
| 2 | `test_voidPlaceOder` |  |
| 3 | `test_refundOder` |  |

## 关联关系
- **覆盖的场景**:[[scn_online_business_cashier_pay]]
- **针对/跑在的服务**:[[svc_cashierii]]、[[svc_acquireii]]、[[svc_tradeii]]、[[svc_payment]]、[[svc_member]]、[[svc_cards]]

## 使用方式
- 入口:`pytest testcases/payment/toB/test_smart_pos.py`;markers:`uat`/`sim`/`regression`。
- 依赖夹具:`get_env`/`get_urls`/`get_env_data`/`db_instance_factory`/`get_testdata`;业务封装 `CGSapi`/`SGS`/`Module`。

## 来源与置信
- cgs-apitest 仓 `toB/test_smart_pos.py`;TC 列表来自源码(allure.title/函数名)。
