---
id: auto_channel_cko_fundIn
object_type: AutomationAsset
name: CKO 充值入金自动化
aliases: [test_cko_fundIn_fangyong]
domain: channel
status: active
owner: unassigned
reviewer: unassigned
last_reviewed_at: '2026-06-24'
source_type: repo
source_ref: cgs-apitest/testcases/payment/fundChannel/test_cko_fundIn_fangyong.py
tags: [channel, 自动化, cgs-apitest]
related_scenarios: [scn_channel_fund_in]
related_services: [svc_qpay_cko, svc_qpay_mpgs, svc_acquireii, svc_tradeii, svc_payment]
---

# CKO 充值入金自动化

> 来源 cgs-apitest `fundChannel/test_cko_fundIn_fangyong.py`(1 TC)。覆盖 [[scn_channel_fund_in]]。

## 用途
对「渠道充值入金 (Fund-In)」做端到端回归(pytest + allure)。

## 用例(TC)
| # | 用例 | 标题 |
| --- | --- | --- |
| 1 | `test_cko101_3ds_cvv_AFT_success` |  |

## 关联关系
- **覆盖的场景**:[[scn_channel_fund_in]]
- **针对/跑在的服务**:[[svc_qpay_cko]]、[[svc_qpay_mpgs]]、[[svc_acquireii]]、[[svc_tradeii]]、[[svc_payment]]

## 使用方式
- 入口:`pytest testcases/payment/fundChannel/test_cko_fundIn_fangyong.py`;markers:`uat`/`sim`/`regression`。

## 来源与置信
- cgs-apitest 仓 `fundChannel/test_cko_fundIn_fangyong.py`;TC 来自源码。
