---
id: auto_wallet_friend_transfer
object_type: AutomationAsset
name: 好友转账自动化
aliases: [test_friend_transfer_jianfei]
domain: wallet
status: active
owner: qianlong.wang
reviewer: qianlong.wang
last_reviewed_at: '2026-06-24'
source_type: repo
source_ref: cgs-apitest/testcases/payment/toC/test_friend_transfer_jianfei.py
tags: [wallet, 支付, 自动化, cgs-apitest]
related_scenarios: [scn_wallet_p2p]
related_services: [svc_member, svc_tradeii, svc_payment, svc_cashierii]
---

# 好友转账自动化

> 来源 cgs-apitest 回归套件 `toC/test_friend_transfer_jianfei.py`(16 TC)。覆盖场景 [[scn_wallet_p2p]]。

## 用途
对「钱包 P2P 转账 / 红包 (Transfer & Red Packet)」做端到端回归(pytest + allure)。

## 用例(TC)
| # | 用例 | 标题 |
| --- | --- | --- |
| 1 | `test_friendTransfer_kycTokyc` |  |
| 2 | `test_friendTransfer_kycTovip` |  |
| 3 | `test_friendTransfer_kycToNokyc` |  |
| 4 | `test_friendTransfer_vipTokyc` |  |
| 5 | `test_friendTransfer_vipTovip` |  |
| 6 | `test_friendTransfer_vipToNokyc` |  |
| 7 | `test_friendTransfer_kycReceipt` |  |
| 8 | `test_friendTransfer_vipReceipt` |  |
| 9 | `test_friendTransfer_kycReject` |  |
| 10 | `test_friendTransfer_vipReject` |  |
| 11 | `test_friendTransfer_bandCardPay` |  |
| 12 | `test_friendTransfer_cashierPay` | N202:KYC User - Balance Payment |
| 13 | `test_friendTransfer_cashier_cardPay` | N203:KYC User - bank card Payment  |
| 14 | `test_friendTransfer_NotAccepted` |  |
| 15 | `test_friendTransfer_NoKYCAccepted` |  |
| 16 | `test_friendTransfer_E103` |  |

## 关联关系
- **覆盖的场景**:[[scn_wallet_p2p]]
- **针对/跑在的服务**:[[svc_member]]、[[svc_tradeii]]、[[svc_payment]]、[[svc_cashierii]]

## 使用方式
- 入口:`pytest testcases/payment/toC/test_friend_transfer_jianfei.py`;markers:`uat`/`sim`/`regression`。
- 依赖夹具:`get_env`/`get_urls`/`get_env_data`/`db_instance_factory`/`get_testdata`;业务封装 `CGSapi`/`SGS`/`Module`。

## 来源与置信
- cgs-apitest 仓 `toC/test_friend_transfer_jianfei.py`;TC 列表来自源码(allure.title/函数名)。
