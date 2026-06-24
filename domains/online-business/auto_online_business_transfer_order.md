---
id: auto_online_business_transfer_order
object_type: AutomationAsset
name: 转账下单自动化
aliases: [test_transfer_order_fangyong]
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-06-24'
source_type: repo
source_ref: cgs-apitest/testcases/payment/toB/test_transfer_order_fangyong.py
tags: [online-business, 支付, 自动化, cgs-apitest]
related_scenarios: [scn_online_business_merchant_payout]
related_services: [svc_fundout, svc_merchant_fundout, svc_remittance, svc_tradeii, svc_payment, svc_cards]
---

# 转账下单自动化

> 来源 cgs-apitest 回归套件 `toB/test_transfer_order_fangyong.py`(4 TC)。覆盖场景 [[scn_online_business_merchant_payout]]。

## 用途
对「商户出款 / 转账 (Transfer / Payout)」做端到端回归(pytest + allure)。

## 用例(TC)
| # | 用例 | 标题 |
| --- | --- | --- |
| 1 | `test_placeTransferOrder_phoneNo` | N101:placeTransferOrder to phoneNo |
| 2 | `test_placeTransferOrder_TOTOKUID` | N102:placeTransferOrder to TOTOKUID |
| 3 | `test_placeTransferOrder_MID_To_Company` | N103:placeTransferOrder to Company MID |
| 4 | `test_placeTransferOrder_MID_To_Personal` | N104:placeTransferOrder to Personal MID |

## 关联关系
- **覆盖的场景**:[[scn_online_business_merchant_payout]]
- **针对/跑在的服务**:[[svc_fundout]]、[[svc_merchant_fundout]]、[[svc_remittance]]、[[svc_tradeii]]、[[svc_payment]]、[[svc_cards]]

## 使用方式
- 入口:`pytest testcases/payment/toB/test_transfer_order_fangyong.py`;markers:`uat`/`sim`/`regression`。
- 依赖夹具:`get_env`/`get_urls`/`get_env_data`/`db_instance_factory`/`get_testdata`;业务封装 `CGSapi`/`SGS`/`Module`。

## 来源与置信
- cgs-apitest 仓 `toB/test_transfer_order_fangyong.py`;TC 列表来自源码(allure.title/函数名)。
