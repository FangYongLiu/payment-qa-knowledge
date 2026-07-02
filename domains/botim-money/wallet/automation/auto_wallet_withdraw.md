---
id: auto_wallet_withdraw
object_type: AutomationAsset
name: 钱包提现自动化
aliases: [test_withdraw_xiaoyan]
domain: wallet
status: active
owner: qianlong.wang
reviewer: qianlong.wang
last_reviewed_at: '2026-06-24'
source_type: repo
source_ref: cgs-apitest/testcases/payment/toC/test_withdraw_xiaoyan.py
tags: [wallet, 支付, 自动化, cgs-apitest]
related_scenarios: [scn_wallet_withdraw]
related_services: [svc_member, svc_tradeii, svc_payment, svc_pfs_payment]
---

# 钱包提现自动化

> 来源 cgs-apitest 回归套件 `toC/test_withdraw_xiaoyan.py`(4 TC)。覆盖场景 [[scn_wallet_withdraw]]。

## 用途
对「钱包提现 (Withdraw)」做端到端回归(pytest + allure)。

## 用例(TC)
| # | 用例 | 标题 |
| --- | --- | --- |
| 1 | `test_kyc_withdraw_bound` | N101:KYC User Withdrawal - Card Already Bound |
| 2 | `test_vip_withdraw_bound` | VIP User Withdrawal - Card Already Bound |
| 3 | `test_kyc_withdraw_new` | KYC User Withdrawal - Bind new IBAN |
| 4 | `test_vvip_withdraw_new` | VVIP User Withdrawal - Bind new IBAN |

## 关联关系
- **覆盖的场景**:[[scn_wallet_withdraw]]
- **针对/跑在的服务**:[[svc_member]]、[[svc_tradeii]]、[[svc_payment]]、[[svc_pfs_payment]]

## 使用方式
- 入口:`pytest testcases/payment/toC/test_withdraw_xiaoyan.py`;markers:`uat`/`sim`/`regression`。
- 依赖夹具:`get_env`/`get_urls`/`get_env_data`/`db_instance_factory`/`get_testdata`;业务封装 `CGSapi`/`SGS`/`Module`。

## 来源与置信
- cgs-apitest 仓 `toC/test_withdraw_xiaoyan.py`;TC 列表来自源码(allure.title/函数名)。
