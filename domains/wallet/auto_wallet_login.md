---
id: auto_wallet_login
object_type: AutomationAsset
name: 登录自动化
aliases: [test_login_xiaoyan]
domain: wallet
status: active
owner: qianlong.wang
reviewer: qianlong.wang
last_reviewed_at: '2026-06-24'
source_type: repo
source_ref: cgs-apitest/testcases/payment/basic_cases/test_login_xiaoyan.py
tags: [wallet, 自动化, cgs-apitest]
related_scenarios: [scn_wallet_account_mgmt]
related_services: [svc_member, svc_cgs, svc_sgs, svc_kyc]
---

# 登录自动化

> 来源 cgs-apitest `basic_cases/test_login_xiaoyan.py`(6 TC)。覆盖 [[scn_wallet_account_mgmt]]。

## 用途
对「账户 / 会员管理 (Account & Member)」做端到端回归(pytest + allure)。

## 用例(TC)
| # | 用例 | 标题 |
| --- | --- | --- |
| 1 | `test_regist_by_opt` | test case N101:Unregistered user mobile phone number + OTP login + set password |
| 2 | `test_login_by_password` | test case N102: Login with old user password |
| 3 | `test_login_setPassword` | test case N103:Registered user phone number + set password to log in |
| 4 | `test_login_by_otp` |  |
| 5 | `test_regist_by_silent` | test case N105: Silent registration BOTIM login mode |
| 6 | `test_login_by_silent` | test case N107: Silent login BOTIM login mode |

## 关联关系
- **覆盖的场景**:[[scn_wallet_account_mgmt]]
- **针对/跑在的服务**:[[svc_member]]、[[svc_cgs]]、[[svc_sgs]]、[[svc_kyc]]

## 使用方式
- 入口:`pytest testcases/payment/basic_cases/test_login_xiaoyan.py`;markers:`uat`/`sim`/`regression`。

## 来源与置信
- cgs-apitest 仓 `basic_cases/test_login_xiaoyan.py`;TC 来自源码。
