---
id: auto_payment_tools_setDeductChannel
object_type: AutomationAsset
name: 代扣渠道设置自动化
aliases: [test_setDeductChannel_xiaoyan]
domain: payment-tools
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-24'
source_type: repo
source_ref: cgs-apitest/testcases/payment/basic_cases/test_setDeductChannel_xiaoyan.py
tags: [payment-tools, 自动化, cgs-apitest]
related_scenarios: [scn_payment_tools_deduct_channel]
related_services: [svc_deduct, svc_member, svc_payment]
---

# 代扣渠道设置自动化

> 来源 cgs-apitest `basic_cases/test_setDeductChannel_xiaoyan.py`(5 TC)。覆盖 [[scn_payment_tools_deduct_channel]]。

## 用途
对「代扣渠道设置 (Deduct Channel)」做端到端回归(pytest + allure)。

## 用例(TC)
| # | 用例 | 标题 |
| --- | --- | --- |
| 1 | `test_set_pay_deduct_balance` | test case1:Set payment order and deduction order |
| 2 | `test_set_pay_deduct_card` | test case2: Set payment order and deduction order |
| 3 | `test_set_pay_deduct_AutoDebit_balance` | test case3: Set payment order and deduction order |
| 4 | `test_set_pay_deduct_AutoDebit_card` | test case4:Set payment order and deduction order |
| 5 | `test_query_balance` | test case5: Check balance |

## 关联关系
- **覆盖的场景**:[[scn_payment_tools_deduct_channel]]
- **针对/跑在的服务**:[[svc_deduct]]、[[svc_member]]、[[svc_payment]]

## 使用方式
- 入口:`pytest testcases/payment/basic_cases/test_setDeductChannel_xiaoyan.py`;markers:`uat`/`sim`/`regression`。

## 来源与置信
- cgs-apitest 仓 `basic_cases/test_setDeductChannel_xiaoyan.py`;TC 来自源码。
