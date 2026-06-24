---
id: auto_wallet_member_xinwei
object_type: AutomationAsset
name: 会员信息自动化
aliases: [test_member_xinwei]
domain: wallet
status: active
owner: qianlong.wang
reviewer: qianlong.wang
last_reviewed_at: '2026-06-24'
source_type: repo
source_ref: cgs-apitest/testcases/payment/basic_cases/test_member_xinwei.py
tags: [wallet, 自动化, cgs-apitest]
related_scenarios: [scn_wallet_account_mgmt]
related_services: [svc_member, svc_cgs, svc_sgs, svc_kyc]
---

# 会员信息自动化

> 来源 cgs-apitest `basic_cases/test_member_xinwei.py`(7 TC)。覆盖 [[scn_wallet_account_mgmt]]。

## 用途
对「账户 / 会员管理 (Account & Member)」做端到端回归(pytest + allure)。

## 用例(TC)
| # | 用例 | 标题 |
| --- | --- | --- |
| 1 | `test_queryBillList` |  |
| 2 | `test_queryBillList` |  |
| 3 | `test_queryBillDetail` |  |
| 4 | `test_queryAvatar` |  |
| 5 | `test_queryAvatarN102` |  |
| 6 | `test_Tips_E101` |  |
| 7 | `test_Tips_E102` |  |

## 关联关系
- **覆盖的场景**:[[scn_wallet_account_mgmt]]
- **针对/跑在的服务**:[[svc_member]]、[[svc_cgs]]、[[svc_sgs]]、[[svc_kyc]]

## 使用方式
- 入口:`pytest testcases/payment/basic_cases/test_member_xinwei.py`;markers:`uat`/`sim`/`regression`。

## 来源与置信
- cgs-apitest 仓 `basic_cases/test_member_xinwei.py`;TC 来自源码。
