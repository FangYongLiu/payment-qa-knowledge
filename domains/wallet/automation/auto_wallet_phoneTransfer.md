---
id: auto_wallet_phoneTransfer
object_type: AutomationAsset
name: 手机号转账自动化
aliases: [test_phoneTransfer_xiaoyan]
domain: wallet
status: active
owner: qianlong.wang
reviewer: qianlong.wang
last_reviewed_at: '2026-06-24'
source_type: repo
source_ref: cgs-apitest/testcases/payment/toC/test_phoneTransfer_xiaoyan.py
tags: [wallet, 支付, 自动化, cgs-apitest]
related_scenarios: [scn_wallet_p2p]
related_services: [svc_member, svc_tradeii, svc_payment, svc_cashierii]
---

# 手机号转账自动化

> 来源 cgs-apitest 回归套件 `toC/test_phoneTransfer_xiaoyan.py`(5 TC)。覆盖场景 [[scn_wallet_p2p]]。

## 用途
对「钱包 P2P 转账 / 红包 (Transfer & Red Packet)」做端到端回归(pytest + allure)。

## 用例(TC)
| # | 用例 | 标题 |
| --- | --- | --- |
| 1 | `test_KYCTransferToKYC` |  |
| 2 | `test_KYCTransferToVIP` |  |
| 3 | `test_KYCTransferToNOKYC` |  |
| 4 | `test_KYCTransfer_Noaccepted` |  |
| 5 | `test_KYCTransfer_payeeAbnormal` |  |

## 关联关系
- **覆盖的场景**:[[scn_wallet_p2p]]
- **针对/跑在的服务**:[[svc_member]]、[[svc_tradeii]]、[[svc_payment]]、[[svc_cashierii]]

## 使用方式
- 入口:`pytest testcases/payment/toC/test_phoneTransfer_xiaoyan.py`;markers:`uat`/`sim`/`regression`。
- 依赖夹具:`get_env`/`get_urls`/`get_env_data`/`db_instance_factory`/`get_testdata`;业务封装 `CGSapi`/`SGS`/`Module`。

## 来源与置信
- cgs-apitest 仓 `toC/test_phoneTransfer_xiaoyan.py`;TC 列表来自源码(allure.title/函数名)。
