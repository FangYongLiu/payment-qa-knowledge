---
id: auto_wallet_f5_whitelist_gating
object_type: AutomationAsset
name: ZAND 白名单灰度自动化
aliases: [test_f5_whitelist_gating]
domain: wallet
status: active
owner: qianlong.wang
reviewer: qianlong.wang
last_reviewed_at: '2026-06-24'
source_type: repo
source_ref: cgs-apitest/testcases/payment/zand_migration/test_f5_whitelist_gating.py
tags: [wallet, 自动化, cgs-apitest]
related_scenarios: [scn_wallet_zand_iban_migration]
related_services: [svc_vis, svc_member, svc_kyc]
---

# ZAND 白名单灰度自动化

> 来源 cgs-apitest `zand_migration/test_f5_whitelist_gating.py`(8 TC)。覆盖 [[scn_wallet_zand_iban_migration]]。

## 用途
对「ZAND IBAN 迁移 (ZAND Migration)」做端到端回归(pytest + allure)。

## 用例(TC)
| # | 用例 | 标题 |
| --- | --- | --- |
| 1 | `test_f5_001_whitelisted_member_auto_open` | TC-F5-001: Whitelisted member gets ZAND IBAN auto-opened |
| 2 | `test_f5_002_non_whitelisted_member_blocked` | TC-F5-002: Non-whitelisted member does NOT get ZAND IBAN |
| 3 | `test_f5_003_non_whitelisted_api_init` | TC-F5-003: Non-whitelisted member — /auth/init returns no ZAND VA |
| 4 | `test_f5_004_whitelisted_api_init` | TC-F5-004: Whitelisted member — /auth/init returns ZAND VA info |
| 5 | `test_f5_005_whitelisted_merchant_migration` | TC-F5-005: Whitelisted merchant — FAB→ZAND migration proceeds |
| 6 | `test_f5_006_non_whitelisted_merchant_blocked` | TC-F5-006: Non-whitelisted merchant — migration NOT triggered |
| 7 | `test_f5_007_non_whitelisted_active_blocked` | TC-F5-007: Non-whitelisted member — /auth/active does not create ZAND VA |
| 8 | `test_f5_008_whitelisted_query_info` | TC-F5-008: Whitelisted member — /query-info returns ZAND IBAN details |

## 关联关系
- **覆盖的场景**:[[scn_wallet_zand_iban_migration]]
- **针对/跑在的服务**:[[svc_vis]]、[[svc_member]]、[[svc_kyc]]

## 使用方式
- 入口:`pytest testcases/payment/zand_migration/test_f5_whitelist_gating.py`;markers:`uat`/`sim`/`regression`。

## 来源与置信
- cgs-apitest 仓 `zand_migration/test_f5_whitelist_gating.py`;TC 来自源码。
