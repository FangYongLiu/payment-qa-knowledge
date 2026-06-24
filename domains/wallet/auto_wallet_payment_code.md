---
id: auto_wallet_payment_code
object_type: AutomationAsset
name: 付款码自动化
aliases: [test_payment_code_pengfei]
domain: wallet
status: active
owner: qianlong.wang
reviewer: qianlong.wang
last_reviewed_at: '2026-06-24'
source_type: repo
source_ref: cgs-apitest/testcases/payment/toC/test_payment_code_pengfei.py
tags: [wallet, 支付, 自动化, cgs-apitest]
related_scenarios: [scn_wallet_consumer_pay]
related_services: [svc_tradeii, svc_payment, svc_member, svc_cashierii]
---

# 付款码自动化

> 来源 cgs-apitest 回归套件 `toC/test_payment_code_pengfei.py`(7 TC)。覆盖场景 [[scn_wallet_consumer_pay]]。

## 用途
对「消费者付款 (Payment Code / PPC)」做端到端回归(pytest + allure)。

## 用例(TC)
| # | 用例 | 标题 |
| --- | --- | --- |
| 1 | `test_paymentCode_withoutAmount` |  |
| 2 | `test_paymentCode_SetAmount` |  |
| 3 | `test_paymentCode_KYCToKYC` |  |
| 4 | `test_paymentCode_withoutKYC` |  |
| 5 | `test_paymentCode_Scanmyself` |  |
| 6 | `test_paymentCode_ScanNoKYC` |  |
| 7 | `test_paymentCode_payeeKYC_payerNoKYC` |  |

## 关联关系
- **覆盖的场景**:[[scn_wallet_consumer_pay]]
- **针对/跑在的服务**:[[svc_tradeii]]、[[svc_payment]]、[[svc_member]]、[[svc_cashierii]]

## 使用方式
- 入口:`pytest testcases/payment/toC/test_payment_code_pengfei.py`;markers:`uat`/`sim`/`regression`。
- 依赖夹具:`get_env`/`get_urls`/`get_env_data`/`db_instance_factory`/`get_testdata`;业务封装 `CGSapi`/`SGS`/`Module`。

## 来源与置信
- cgs-apitest 仓 `toC/test_payment_code_pengfei.py`;TC 列表来自源码(allure.title/函数名)。
