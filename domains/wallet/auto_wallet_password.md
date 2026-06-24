---
id: auto_wallet_password
object_type: AutomationAsset
name: 密码自动化
aliases: [test_password_xiaoyan]
domain: wallet
status: active
owner: qianlong.wang
reviewer: qianlong.wang
last_reviewed_at: '2026-06-24'
source_type: repo
source_ref: cgs-apitest/testcases/payment/basic_cases/test_password_xiaoyan.py
tags: [wallet, 自动化, cgs-apitest]
related_scenarios: [scn_wallet_account_mgmt]
related_services: [svc_member, svc_cgs, svc_sgs, svc_kyc]
---

# 密码自动化

> 来源 cgs-apitest `basic_cases/test_password_xiaoyan.py`(6 TC)。覆盖 [[scn_wallet_account_mgmt]]。

## 用途
对「账户 / 会员管理 (Account & Member)」做端到端回归(pytest + allure)。

## 用例(TC)
| # | 用例 | 标题 |
| --- | --- | --- |
| 1 | `test_set_password_cashier` | test case1: No payment password is set, go through the cashier transaction process |
| 2 | `test_set_password` | test case2: botim login and set password |
| 3 | `test_modify_password` | test case3: botim login and modify password |
| 4 | `test_forget_password_no_login` | test case4: Forgot password if not logged in payby |
| 5 | `test_forget_password` | test case5: botim login and fotget password |
| 6 | `test_forget_password_cashier` | test case6: Botim login use case - cashier forgot password |

## 关联关系
- **覆盖的场景**:[[scn_wallet_account_mgmt]]
- **针对/跑在的服务**:[[svc_member]]、[[svc_cgs]]、[[svc_sgs]]、[[svc_kyc]]

## 使用方式
- 入口:`pytest testcases/payment/basic_cases/test_password_xiaoyan.py`;markers:`uat`/`sim`/`regression`。

## 来源与置信
- cgs-apitest 仓 `basic_cases/test_password_xiaoyan.py`;TC 来自源码。
