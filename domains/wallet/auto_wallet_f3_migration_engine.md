---
id: auto_wallet_f3_migration_engine
object_type: AutomationAsset
name: ZAND 迁移引擎自动化
aliases: [test_f3_migration_engine]
domain: wallet
status: active
owner: qianlong.wang
reviewer: qianlong.wang
last_reviewed_at: '2026-06-24'
source_type: repo
source_ref: cgs-apitest/testcases/payment/zand_migration/test_f3_migration_engine.py
tags: [wallet, 自动化, cgs-apitest]
related_scenarios: [scn_wallet_zand_iban_migration]
related_services: [svc_vis, svc_member, svc_kyc]
---

# ZAND 迁移引擎自动化

> 来源 cgs-apitest `zand_migration/test_f3_migration_engine.py`(3 TC)。覆盖 [[scn_wallet_zand_iban_migration]]。

## 用途
对「ZAND IBAN 迁移 (ZAND Migration)」做端到端回归(pytest + allure)。

## 用例(TC)
| # | 用例 | 标题 |
| --- | --- | --- |
| 1 | `test_f3_001_migration_happy_flow` | TC-F3-001: Migration happy flow — PENDING → COMPLETED |
| 2 | `test_f3_002_migration_failure` | TC-F3-002: Migration failure — PENDING → FAILED |
| 3 | `test_f3_009_fab_iban_mapping_update` | TC-F3-009: FAB IBAN mapping update after successful migration |

## 关联关系
- **覆盖的场景**:[[scn_wallet_zand_iban_migration]]
- **针对/跑在的服务**:[[svc_vis]]、[[svc_member]]、[[svc_kyc]]

## 使用方式
- 入口:`pytest testcases/payment/zand_migration/test_f3_migration_engine.py`;markers:`uat`/`sim`/`regression`。

## 来源与置信
- cgs-apitest 仓 `zand_migration/test_f3_migration_engine.py`;TC 来自源码。
