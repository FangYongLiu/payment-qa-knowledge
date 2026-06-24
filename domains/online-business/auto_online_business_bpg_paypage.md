---
id: auto_online_business_bpg_paypage
object_type: AutomationAsset
name: 收银台 BPG PayPage 自动化
aliases: [test_bpg_paypage_fangyong]
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-06-24'
source_type: repo
source_ref: cgs-apitest/testcases/payment/toB/test_bpg_paypage_fangyong.py
tags: [online-business, 支付, 自动化, cgs-apitest]
related_scenarios: [scn_online_business_cashier_pay]
related_services: [svc_cashierii, svc_acquireii, svc_tradeii, svc_payment, svc_member, svc_cards]
---

# 收银台 BPG PayPage 自动化

> 来源 cgs-apitest 回归套件 `toB/test_bpg_paypage_fangyong.py`(15 TC)。覆盖场景 [[scn_online_business_cashier_pay]]。

## 用途
对「收银台支付 (Cashier / PayPage)」做端到端回归(pytest + allure)。

## 用例(TC)
| # | 用例 | 标题 |
| --- | --- | --- |
| 1 | `test_anonymous_card_payment_n101` |  |
| 2 | `test_qr_pay_with_balance_n102` |  |
| 3 | `test_qr_bind_new_card_and_pay_n103` |  |
| 4 | `test_qr_pay_with_bound_card_n104` |  |
| 5 | `test_bind_new_card_with_customer_id_then_unbind_n105` |  |
| 6 | `test_pay_with_stored_card_by_customer_id_n106` |  |
| 7 | `test_mobile_login_bind_card_payment_n107` |  |
| 8 | `test_mobile_login_stored_card_payment_n108` |  |
| 9 | `test_anonymous_card_dcc_accepted_payment_n109` |  |
| 10 | `test_mobile_login_bind_card_dcc_accepted_payment_n110` |  |
| 11 | `test_mobile_login_stored_card_dcc_accepted_payment_n111` |  |
| 12 | `test_anonymous_card_dcc_declined_payment_n112` |  |
| 13 | `test_anonymous_card_payment_refund_e101` |  |
| 14 | `test_qr_pay_with_balance_and_refund_e102` |  |
| 15 | `test_qr_pay_with_bound_card_and_refund_e103` |  |

## 关联关系
- **覆盖的场景**:[[scn_online_business_cashier_pay]]
- **针对/跑在的服务**:[[svc_cashierii]]、[[svc_acquireii]]、[[svc_tradeii]]、[[svc_payment]]、[[svc_member]]、[[svc_cards]]

## 使用方式
- 入口:`pytest testcases/payment/toB/test_bpg_paypage_fangyong.py`;markers:`uat`/`sim`/`regression`。
- 依赖夹具:`get_env`/`get_urls`/`get_env_data`/`db_instance_factory`/`get_testdata`;业务封装 `CGSapi`/`SGS`/`Module`。

## 来源与置信
- cgs-apitest 仓 `toB/test_bpg_paypage_fangyong.py`;TC 列表来自源码(allure.title/函数名)。
