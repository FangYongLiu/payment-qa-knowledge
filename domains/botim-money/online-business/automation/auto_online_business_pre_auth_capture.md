---
id: auto_online_business_pre_auth_capture
object_type: AutomationAsset
name: 预授权/请款自动化
aliases: [test_pre_auth_capture_fangyong]
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-06-24'
source_type: repo
source_ref: cgs-apitest/testcases/payment/toB/test_pre_auth_capture_fangyong.py
tags: [online-business, 支付, 自动化, cgs-apitest]
related_scenarios: [scn_online_business_pre_auth]
related_services: [svc_acquireii, svc_tradeii, svc_payment, svc_cards, svc_acs]
---

# 预授权/请款自动化

> 来源 cgs-apitest 回归套件 `toB/test_pre_auth_capture_fangyong.py`(8 TC)。覆盖场景 [[scn_online_business_pre_auth]]。

## 用途
对「预授权 / 请款 (PreAuth-Capture)」做端到端回归(pytest + allure)。

## 用例(TC)
| # | 用例 | 标题 |
| --- | --- | --- |
| 1 | `test_PreAuthCapture_bindCard` | N101:PreAuthCapture bindCard |
| 2 | `test_PreAuthCapture_CardToken_MOTO_cvv` | N102:PreAuthCapture CardToken MOTO CVV |
| 3 | `test_PreAuthCapture_CardToken_MOTO_NoCvv` | N103:PreAuthCapture CardToken MOTO NoCVV |
| 4 | `test_PreAuth_Void` | N104:PreAuth Void |
| 5 | `test_preAuth_Partially_Capture` | N105:PreAuth Partially Capture |
| 6 | `test_PreAuthCapture_FullRefund` | N106:PreAuthCapture Full Refund |
| 7 | `test_PreAuthCapture_Partially_Refund` | N107:PreAuthCapture Partially Refund |
| 8 | `test_PreAuthCapture_bindCard_3Ds_Downgrade` | N108:PreAuthCapture bindCard 3Ds Downgrade |

## 关联关系
- **覆盖的场景**:[[scn_online_business_pre_auth]]
- **针对/跑在的服务**:[[svc_acquireii]]、[[svc_tradeii]]、[[svc_payment]]、[[svc_cards]]、[[svc_acs]]

## 使用方式
- 入口:`pytest testcases/payment/toB/test_pre_auth_capture_fangyong.py`;markers:`uat`/`sim`/`regression`。
- 依赖夹具:`get_env`/`get_urls`/`get_env_data`/`db_instance_factory`/`get_testdata`;业务封装 `CGSapi`/`SGS`/`Module`。

## 来源与置信
- cgs-apitest 仓 `toB/test_pre_auth_capture_fangyong.py`;TC 列表来自源码(allure.title/函数名)。
