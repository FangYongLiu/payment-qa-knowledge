---
id: auto_wallet_f4_notification
object_type: AutomationAsset
name: ZAND 迁移通知自动化
aliases: [test_f4_notification_todo]
domain: wallet
status: active
owner: qianlong.wang
reviewer: qianlong.wang
last_reviewed_at: '2026-06-24'
source_type: repo
source_ref: cgs-apitest/testcases/payment/zand_migration/test_f4_notification_todo.py
tags: [wallet, 自动化, cgs-apitest]
related_scenarios: [scn_wallet_zand_iban_migration]
related_services: [svc_vis, svc_member, svc_kyc]
---

# ZAND 迁移通知自动化

> 来源 cgs-apitest `zand_migration/test_f4_notification_todo.py`(10 TC)。覆盖 [[scn_wallet_zand_iban_migration]]。

## 用途
对「ZAND IBAN 迁移 (ZAND Migration)」做端到端回归(pytest + allure)。

## 用例(TC)
| # | 用例 | 标题 |
| --- | --- | --- |
| 1 | `test_f4_001_m_type_notification_triggered` | TC-F4-001: Notification triggered for M-type (FAB→ZAND migration) |
| 2 | `test_f4_002_n_type_notification_triggered` | TC-F4-002: Notification triggered for N-type (new ZAND IBAN) |
| 3 | `test_f4_003_m_type_todo_card` | TC-F4-003: ToDo card created for M-type via /personal/notice/pull |
| 4 | `test_f4_004_n_type_todo_card` | TC-F4-004: ToDo card created for N-type via /personal/notice/pull |
| 5 | `test_f4_005_todo_removal_after_deposit` | TC-F4-005: ToDo card removal after deposit — notify_status S→R |
| 6 | `test_f4_006_todo_removal_60_days` | TC-F4-006: ToDo card auto-removal after 60 days elapsed |
| 7 | `test_f4_007_m_type_notification_content` | TC-F4-007: Notification content verification for M-type |
| 8 | `test_f4_008_n_type_notification_content` | TC-F4-008: Notification content verification for N-type |
| 9 | `test_f4_009_notify_status_state_machine` | TC-F4-009: notify_status state machine verification |
| 10 | `test_f4_010_no_duplicate_notifications` | TC-F4-010: No duplicate notifications for same user |

## 关联关系
- **覆盖的场景**:[[scn_wallet_zand_iban_migration]]
- **针对/跑在的服务**:[[svc_vis]]、[[svc_member]]、[[svc_kyc]]

## 使用方式
- 入口:`pytest testcases/payment/zand_migration/test_f4_notification_todo.py`;markers:`uat`/`sim`/`regression`。

## 来源与置信
- cgs-apitest 仓 `zand_migration/test_f4_notification_todo.py`;TC 来自源码。
