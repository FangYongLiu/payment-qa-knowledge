---
id: auto_wallet_f1_auto_open_zand_iban
object_type: AutomationAsset
name: ZAND IBAN 自动开户自动化
aliases: [test_f1_auto_open_zand_iban]
domain: wallet
status: active
owner: qianlong.wang
reviewer: qianlong.wang
last_reviewed_at: '2026-06-24'
source_type: repo
source_ref: cgs-apitest/testcases/payment/zand_migration/test_f1_auto_open_zand_iban.py
tags: [wallet, 自动化, cgs-apitest]
related_scenarios: [scn_wallet_zand_iban_migration]
related_services: [svc_vis, svc_member, svc_kyc]
---

# ZAND IBAN 自动开户自动化

> 来源 cgs-apitest `zand_migration/test_f1_auto_open_zand_iban.py`(6 TC)。覆盖 [[scn_wallet_zand_iban_migration]]。

## 用途
对「ZAND IBAN 迁移 (ZAND Migration)」做端到端回归(pytest + allure)。

## 用例(TC)
| # | 用例 | 标题 |
| --- | --- | --- |
| 1 | `test_f1_001_normal_kyc_auto_open` | TC-F1-001: Normal KYC user auto-open ZAND IBAN - Happy flow |
| 2 | `test_f1_010_standard_kyc_individual` | TC-F1-010: KYC Scenario (a) - Standard KYC Individual auto-open ZAND IBAN |
| 3 | `test_f1_002_vip_kyc_auto_open` | TC-F1-002: VIP KYC user auto-open ZAND IBAN |
| 4 | `test_f1_011_vip_kyc_individual` | TC-F1-011: KYC Scenario (b) - VIP KYC Individual auto-open ZAND IBAN |
| 5 | `test_f1_003_zand_api_error` | TC-F1-003: ZAND API connect error during auto-open |
| 6 | `test_f1_012_manual_review_approved` | TC-F1-012: KYC Scenario (c) - Manual Review → Approved auto-open ZAND IBAN |

## 关联关系
- **覆盖的场景**:[[scn_wallet_zand_iban_migration]]
- **针对/跑在的服务**:[[svc_vis]]、[[svc_member]]、[[svc_kyc]]

## 使用方式
- 入口:`pytest testcases/payment/zand_migration/test_f1_auto_open_zand_iban.py`;markers:`uat`/`sim`/`regression`。

## 来源与置信
- cgs-apitest 仓 `zand_migration/test_f1_auto_open_zand_iban.py`;TC 来自源码。
