---
id: auto_wallet_delete_account
object_type: AutomationAsset
name: 注销账户自动化
aliases: [test_delete_account_xiaoyan]
domain: wallet
status: active
owner: qianlong.wang
reviewer: qianlong.wang
last_reviewed_at: '2026-06-24'
source_type: repo
source_ref: cgs-apitest/testcases/payment/basic_cases/test_delete_account_xiaoyan.py
tags: [wallet, 自动化, cgs-apitest]
related_scenarios: [scn_wallet_account_mgmt]
related_services: [svc_member, svc_cgs, svc_sgs, svc_kyc]
---

# 注销账户自动化

> 来源 cgs-apitest `basic_cases/test_delete_account_xiaoyan.py`(4 TC)。覆盖 [[scn_wallet_account_mgmt]]。

## 用途
对「账户 / 会员管理 (Account & Member)」做端到端回归(pytest + allure)。

## 用例(TC)
| # | 用例 | 标题 |
| --- | --- | --- |
| 1 | `test_deleteAccount` | N101: Normal logout |
| 2 | `test_deleteAccountN103` | N103: Digital currency cancellation |
| 3 | `test_deleteAccountE103` | E103: There are transactions in progress |
| 4 | `test_regist_by_opt` | test case N101:未注册用户手机号+OTP登录+设置密码：【{mobile},{password}】 |

## 关联关系
- **覆盖的场景**:[[scn_wallet_account_mgmt]]
- **针对/跑在的服务**:[[svc_member]]、[[svc_cgs]]、[[svc_sgs]]、[[svc_kyc]]

## 使用方式
- 入口:`pytest testcases/payment/basic_cases/test_delete_account_xiaoyan.py`;markers:`uat`/`sim`/`regression`。

## 来源与置信
- cgs-apitest 仓 `basic_cases/test_delete_account_xiaoyan.py`;TC 来自源码。
