---
id: auto_online_business_merchant_split
object_type: AutomationAsset
name: 商户分账自动化
aliases: [test_merchant_split_fangyong]
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-06-24'
source_type: repo
source_ref: cgs-apitest/testcases/payment/toB/test_merchant_split_fangyong.py
tags: [online-business, 支付, 自动化, cgs-apitest]
related_scenarios: [scn_online_business_merchant_split]
related_services: [svc_tradeii, svc_payment, svc_pfs_payment, svc_merchant]
---

# 商户分账自动化

> 来源 cgs-apitest 回归套件 `toB/test_merchant_split_fangyong.py`(10 TC)。覆盖场景 [[scn_online_business_merchant_split]]。

## 用途
对「商户分账 (Merchant Split)」做端到端回归(pytest + allure)。

## 用例(TC)
| # | 用例 | 标题 |
| --- | --- | --- |
| 1 | `test_merchantSplit_N101` |  |
| 2 | `test_merchantSplit_N102` |  |
| 3 | `test_merchantSplit_N103` |  |
| 4 | `test_merchantSplit_N104` |  |
| 5 | `test_merchantSplit_N105` |  |
| 6 | `test_merchantSplit_N106` |  |
| 7 | `test_merchantSplit_N107` |  |
| 8 | `test_merchantSplit_N108` |  |
| 9 | `test_merchantSplit_N109` |  |
| 10 | `test_merchantSplit_N110` |  |

## 关联关系
- **覆盖的场景**:[[scn_online_business_merchant_split]]
- **针对/跑在的服务**:[[svc_tradeii]]、[[svc_payment]]、[[svc_pfs_payment]]、[[svc_merchant]]

## 使用方式
- 入口:`pytest testcases/payment/toB/test_merchant_split_fangyong.py`;markers:`uat`/`sim`/`regression`。
- 依赖夹具:`get_env`/`get_urls`/`get_env_data`/`db_instance_factory`/`get_testdata`;业务封装 `CGSapi`/`SGS`/`Module`。

## 来源与置信
- cgs-apitest 仓 `toB/test_merchant_split_fangyong.py`;TC 列表来自源码(allure.title/函数名)。
