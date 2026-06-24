---
id: auto_remittance_remittance
object_type: AutomationAsset
name: 跨境汇款自动化
aliases: [test_remittance_pengfei]
domain: remittance
status: active
owner: lei.pan
reviewer: lei.pan
last_reviewed_at: '2026-06-24'
source_type: repo
source_ref: cgs-apitest/testcases/payment/toC/test_remittance_pengfei.py
tags: [remittance, 支付, 自动化, cgs-apitest]
related_scenarios: [scn_remittance_cross_border]
related_services: [svc_remittance, svc_cashierii, svc_tradeii, svc_payment, svc_member]
---

# 跨境汇款自动化

> 来源 cgs-apitest 回归套件 `toC/test_remittance_pengfei.py`(12 TC)。覆盖场景 [[scn_remittance_cross_border]]。

## 用途
对「跨境汇款 (Remittance)」做端到端回归(pytest + allure)。

## 用例(TC)
| # | 用例 | 标题 |
| --- | --- | --- |
| 1 | `test_remittanceN101` |  |
| 2 | `test_remittanceN102` |  |
| 3 | `test_remittanceN103` |  |
| 4 | `test_remittanceN301` |  |
| 5 | `test_remittanceN105` |  |
| 6 | `test_remittanceN106` |  |
| 7 | `test_remittanceN107` |  |
| 8 | `test_remittanceN108` |  |
| 9 | `test_remittanceN109` |  |
| 10 | `test_remittanceN130` |  |
| 11 | `test_remittanceN104` |  |
| 12 | `test_remittanceN135` |  |

## 关联关系
- **覆盖的场景**:[[scn_remittance_cross_border]]
- **针对/跑在的服务**:[[svc_remittance]]、[[svc_cashierii]]、[[svc_tradeii]]、[[svc_payment]]、[[svc_member]]

## 使用方式
- 入口:`pytest testcases/payment/toC/test_remittance_pengfei.py`;markers:`uat`/`sim`/`regression`。
- 依赖夹具:`get_env`/`get_urls`/`get_env_data`/`db_instance_factory`/`get_testdata`;业务封装 `CGSapi`/`SGS`/`Module`。

## 来源与置信
- cgs-apitest 仓 `toC/test_remittance_pengfei.py`;TC 列表来自源码(allure.title/函数名)。
