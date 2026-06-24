---
id: auto_wallet_deposit
object_type: AutomationAsset
name: 钱包充值自动化
aliases: [test_deposit_pengfei]
domain: wallet
status: active
owner: qianlong.wang
reviewer: qianlong.wang
last_reviewed_at: '2026-06-24'
source_type: repo
source_ref: cgs-apitest/testcases/payment/toC/test_deposit_pengfei.py
tags: [wallet, 支付, 自动化, cgs-apitest]
related_scenarios: [scn_wallet_deposit]
related_services: [svc_cashierii, svc_member, svc_tradeii, svc_payment, svc_cards]
---

# 钱包充值自动化

> 来源 cgs-apitest 回归套件 `toC/test_deposit_pengfei.py`(10 TC)。覆盖场景 [[scn_wallet_deposit]]。

## 用途
对「钱包充值 (Deposit / Top-Up)」做端到端回归(pytest + allure)。

## 用例(TC)
| # | 用例 | 标题 |
| --- | --- | --- |
| 1 | `test_deposit_card` | N101:KYC User Card Binding & Deposit  |
| 2 | `test_deposit_hasCard` | N102:Deposit with Bound Card |
| 3 | `test_deposit_Kios_KYC` | N201:Kios - Top-Up for KYC User |
| 4 | `test_deposit_Kios_VIP` | N202:Kios-Top-Up for KYC User |
| 5 | `test_deposit_Kios_Nokyc` | N203:Kios - Top-Up for Non-KYC User |
| 6 | `test_deposit_new_card` | N301:KYC User Top-Up via New Cashier with Card Binding |
| 7 | `test_deposit_new_hasCard` | N302:KYC User Top-Up via New Cashier with Bound Card |
| 8 | `test_deposit_memberStatusAbnormal` | E301:KYC User Account - Basic Account Status Abnormal |
| 9 | `test_deposit_new_NoKYC` | E302: Member NO-KYC |
| 10 | `test_deposit_kycExpired` | E303 KYC Expired |

## 关联关系
- **覆盖的场景**:[[scn_wallet_deposit]]
- **针对/跑在的服务**:[[svc_cashierii]]、[[svc_member]]、[[svc_tradeii]]、[[svc_payment]]、[[svc_cards]]

## 使用方式
- 入口:`pytest testcases/payment/toC/test_deposit_pengfei.py`;markers:`uat`/`sim`/`regression`。
- 依赖夹具:`get_env`/`get_urls`/`get_env_data`/`db_instance_factory`/`get_testdata`;业务封装 `CGSapi`/`SGS`/`Module`。

## 来源与置信
- cgs-apitest 仓 `toC/test_deposit_pengfei.py`;TC 列表来自源码(allure.title/函数名)。
