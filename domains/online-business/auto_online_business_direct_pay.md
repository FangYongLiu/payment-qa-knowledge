---
id: auto_online_business_direct_pay
object_type: AutomationAsset
name: 直连支付自动化
aliases: [test_direct_pay_fangyong]
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-06-24'
source_type: repo
source_ref: cgs-apitest/testcases/payment/toB/test_direct_pay_fangyong.py
tags: [online-business, 支付, 自动化, cgs-apitest]
related_scenarios: [scn_online_business_direct_pay]
related_services: [svc_acquireii, svc_sgs, svc_tradeii, svc_payment, svc_acs, svc_cards, svc_pfs_payment]
---

# 直连支付自动化

> 来源 cgs-apitest 回归套件 `toB/test_direct_pay_fangyong.py`(9 TC)。覆盖场景 [[scn_online_business_direct_pay]]。

## 用途
对「直连支付 (Direct Pay)」做端到端回归(pytest + allure)。

## 用例(TC)
| # | 用例 | 标题 |
| --- | --- | --- |
| 1 | `test_directpay_bindCard` | N101:direct pay bind card |
| 2 | `test_directpay_hasCard` | N102:direct pay with card token |
| 3 | `test_directpay_refund` | N103:direct pay and refund |
| 4 | `test_directpay_PartialRefund` | N104:direct pay and Partial refund |
| 5 | `test_directpay_dcc_accepted_card_payment_n105` | N105: directpay DCC accepted card payment |
| 6 | `test_directpay_dcc_declined_card_payment_n106` | N106: directpay DCC declined card payment |
| 7 | `test_directpay_dcc_invalid_quote_id_partner_rejected_n107` | N107: directpay DCC invalid quoteId partner rejected |
| 8 | `test_directpay_dcc_full_refund_n108` | N108: directpay DCC full refund |
| 9 | `test_directpay_dcc_partial_refund_last_refund_n109` | N109: directpay DCC partial refund last refund |

## 关联关系
- **覆盖的场景**:[[scn_online_business_direct_pay]]
- **针对/跑在的服务**:[[svc_acquireii]]、[[svc_sgs]]、[[svc_tradeii]]、[[svc_payment]]、[[svc_acs]]、[[svc_cards]]、[[svc_pfs_payment]]

## 使用方式
- 入口:`pytest testcases/payment/toB/test_direct_pay_fangyong.py`;markers:`uat`/`sim`/`regression`。
- 依赖夹具:`get_env`/`get_urls`/`get_env_data`/`db_instance_factory`/`get_testdata`;业务封装 `CGSapi`/`SGS`/`Module`。

## 来源与置信
- cgs-apitest 仓 `toB/test_direct_pay_fangyong.py`;TC 列表来自源码(allure.title/函数名)。
