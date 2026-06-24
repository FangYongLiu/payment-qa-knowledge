---
id: auto_card_bankcards
object_type: AutomationAsset
name: 绑卡管理自动化
aliases: [test_bankcards_xiaoyan]
domain: card
status: active
owner: jianfei.wang
reviewer: jianfei.wang
last_reviewed_at: '2026-06-24'
source_type: repo
source_ref: cgs-apitest/testcases/payment/basic_cases/test_bankcards_xiaoyan.py
tags: [card, 自动化, cgs-apitest]
related_scenarios: [scn_card_manage]
related_services: [svc_cards, svc_member]
---

# 绑卡管理自动化

> 来源 cgs-apitest `basic_cases/test_bankcards_xiaoyan.py`(7 TC)。覆盖 [[scn_card_manage]]。

## 用途
对「绑卡管理 (Bank Cards)」做端到端回归(pytest + allure)。

## 用例(TC)
| # | 用例 | 标题 |
| --- | --- | --- |
| 1 | `test_nokyc_bind_cards` |  |
| 2 | `test_kyc_bind_cards` |  |
| 3 | `test_vip_bind_cards` |  |
| 4 | `test_query_cards_list` |  |
| 5 | `test_kyc_bind_iban` |  |
| 6 | `test_vip_bind_iban` |  |
| 7 | `test_vvip_bind_iban` |  |

## 关联关系
- **覆盖的场景**:[[scn_card_manage]]
- **针对/跑在的服务**:[[svc_cards]]、[[svc_member]]

## 使用方式
- 入口:`pytest testcases/payment/basic_cases/test_bankcards_xiaoyan.py`;markers:`uat`/`sim`/`regression`。

## 来源与置信
- cgs-apitest 仓 `basic_cases/test_bankcards_xiaoyan.py`;TC 来自源码。
