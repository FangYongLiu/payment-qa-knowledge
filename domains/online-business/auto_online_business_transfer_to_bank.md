---
id: auto_online_business_transfer_to_bank
object_type: AutomationAsset
name: 转账到银行自动化
aliases: [test_transfer_to_bank_fangyong]
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-06-24'
source_type: repo
source_ref: cgs-apitest/testcases/payment/toB/test_transfer_to_bank_fangyong.py
tags: [online-business, 支付, 自动化, cgs-apitest]
related_scenarios: [scn_online_business_merchant_payout]
related_services: [svc_fundout, svc_merchant_fundout, svc_remittance, svc_tradeii, svc_payment, svc_cards]
---

# 转账到银行自动化

> 来源 cgs-apitest 回归套件 `toB/test_transfer_to_bank_fangyong.py`(3 TC)。覆盖场景 [[scn_online_business_merchant_payout]]。

## 用途
对「商户出款 / 转账 (Transfer / Payout)」做端到端回归(pytest + allure)。

## 用例(TC)
| # | 用例 | 标题 |
| --- | --- | --- |
| 1 | `test_placeTransferToBankOrder_LocalAED` | N101:placeTransferToBankOrder Local AED |
| 2 | `test_placeTransferToBankOrder_LocalUSD` | N102:placeTransferToBankOrder_LocalUSD |
| 3 | `test_placeTransferToBankOrder_SWIFTUSD` | N103:placeTransferToBankOrder_SWIFTUSD |

## 关联关系
- **覆盖的场景**:[[scn_online_business_merchant_payout]]
- **针对/跑在的服务**:[[svc_fundout]]、[[svc_merchant_fundout]]、[[svc_remittance]]、[[svc_tradeii]]、[[svc_payment]]、[[svc_cards]]

## 使用方式
- 入口:`pytest testcases/payment/toB/test_transfer_to_bank_fangyong.py`;markers:`uat`/`sim`/`regression`。
- 依赖夹具:`get_env`/`get_urls`/`get_env_data`/`db_instance_factory`/`get_testdata`;业务封装 `CGSapi`/`SGS`/`Module`。

## 来源与置信
- cgs-apitest 仓 `toB/test_transfer_to_bank_fangyong.py`;TC 列表来自源码(allure.title/函数名)。
