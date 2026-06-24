---
id: auto_wallet_vam_query_api
object_type: AutomationAsset
name: VAM 查询自动化
aliases: [test_vam_query_api]
domain: wallet
status: active
owner: qianlong.wang
reviewer: qianlong.wang
last_reviewed_at: '2026-06-24'
source_type: repo
source_ref: cgs-apitest/testcases/payment/zand_migration/test_vam_query_api.py
tags: [wallet, 自动化, cgs-apitest]
related_scenarios: [scn_wallet_zand_iban_migration]
related_services: [svc_vis, svc_member, svc_kyc]
---

# VAM 查询自动化

> 来源 cgs-apitest `zand_migration/test_vam_query_api.py`(1 TC)。覆盖 [[scn_wallet_zand_iban_migration]]。

## 用途
对「ZAND IBAN 迁移 (ZAND Migration)」做端到端回归(pytest + allure)。

## 用例(TC)
| # | 用例 | 标题 |
| --- | --- | --- |
| 1 | `test_vam_query_info_v2` | T10411: Query accounts - basic + multiple IBAN |

## 关联关系
- **覆盖的场景**:[[scn_wallet_zand_iban_migration]]
- **针对/跑在的服务**:[[svc_vis]]、[[svc_member]]、[[svc_kyc]]

## 使用方式
- 入口:`pytest testcases/payment/zand_migration/test_vam_query_api.py`;markers:`uat`/`sim`/`regression`。

## 来源与置信
- cgs-apitest 仓 `zand_migration/test_vam_query_api.py`;TC 来自源码。
