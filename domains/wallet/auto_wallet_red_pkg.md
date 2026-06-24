---
id: auto_wallet_red_pkg
object_type: AutomationAsset
name: 红包自动化
aliases: [test_red_pkg_jianfei]
domain: wallet
status: active
owner: qianlong.wang
reviewer: qianlong.wang
last_reviewed_at: '2026-06-24'
source_type: repo
source_ref: cgs-apitest/testcases/payment/toC/test_red_pkg_jianfei.py
tags: [wallet, 支付, 自动化, cgs-apitest]
related_scenarios: [scn_wallet_p2p]
related_services: [svc_member, svc_tradeii, svc_payment, svc_cashierii]
---

# 红包自动化

> 来源 cgs-apitest 回归套件 `toC/test_red_pkg_jianfei.py`(8 TC)。覆盖场景 [[scn_wallet_p2p]]。

## 用途
对「钱包 P2P 转账 / 红包 (Transfer & Red Packet)」做端到端回归(pytest + allure)。

## 用例(TC)
| # | 用例 | 标题 |
| --- | --- | --- |
| 1 | `test_SendRedPkg_KYC` |  |
| 2 | `test_vipSendRedPkg_KYCReceive` |  |
| 3 | `test_SendRedPkg_payByNewcard` | N201:VIP user sends a red envelope and receives it themselves, standard checkout binds card for payment |
| 4 | `test_SendRedPkg_payByBlance` | N202：KYC user sends a red envelope, standard checkout uses balance for payment |
| 5 | `test_SendRedPkg_expired` | E101:KYC user sends a red envelope, checkout balance payment expires and is refunded. |
| 6 | `test_SendRedPkg_NoKYCReceive` | E102:KYC user sends a red envelope, NoKYC receives it. |
| 7 | `test_SendRedPkg_NoKYCSend` | E103NoKYC user sends a red envelope, NoKYC receives it |
| 8 | `test_SendRedPkg_partlyExpired` |  |

## 关联关系
- **覆盖的场景**:[[scn_wallet_p2p]]
- **针对/跑在的服务**:[[svc_member]]、[[svc_tradeii]]、[[svc_payment]]、[[svc_cashierii]]

## 使用方式
- 入口:`pytest testcases/payment/toC/test_red_pkg_jianfei.py`;markers:`uat`/`sim`/`regression`。
- 依赖夹具:`get_env`/`get_urls`/`get_env_data`/`db_instance_factory`/`get_testdata`;业务封装 `CGSapi`/`SGS`/`Module`。

## 来源与置信
- cgs-apitest 仓 `toC/test_red_pkg_jianfei.py`;TC 列表来自源码(allure.title/函数名)。
