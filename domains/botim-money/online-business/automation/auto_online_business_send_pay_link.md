---
id: auto_online_business_send_pay_link
object_type: AutomationAsset
name: 发送支付链接自动化
aliases: [test_send_pay_link_fangyong]
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-06-24'
source_type: repo
source_ref: cgs-apitest/testcases/payment/toB/test_send_pay_link_fangyong.py
tags: [online-business, 支付, 自动化, cgs-apitest]
related_scenarios: [scn_online_business_cashier_pay]
related_services: [svc_cashierii, svc_acquireii, svc_tradeii, svc_payment, svc_member, svc_cards]
---

# 发送支付链接自动化

> 来源 cgs-apitest 回归套件 `toB/test_send_pay_link_fangyong.py`(1 TC)。覆盖场景 [[scn_online_business_cashier_pay]]。

## 用途
对「收银台支付 (Cashier / PayPage)」做端到端回归(pytest + allure)。

## 用例(TC)
| # | 用例 | 标题 |
| --- | --- | --- |
| 1 | `test_sendPayLink_email` |  |

## 关联关系
- **覆盖的场景**:[[scn_online_business_cashier_pay]]
- **针对/跑在的服务**:[[svc_cashierii]]、[[svc_acquireii]]、[[svc_tradeii]]、[[svc_payment]]、[[svc_member]]、[[svc_cards]]

## 使用方式
- 入口:`pytest testcases/payment/toB/test_send_pay_link_fangyong.py`;markers:`uat`/`sim`/`regression`。
- 依赖夹具:`get_env`/`get_urls`/`get_env_data`/`db_instance_factory`/`get_testdata`;业务封装 `CGSapi`/`SGS`/`Module`。

## 来源与置信
- cgs-apitest 仓 `toB/test_send_pay_link_fangyong.py`;TC 列表来自源码(allure.title/函数名)。
