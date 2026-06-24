---
id: scn_wallet_zand_iban_migration
object_type: Scenario
name: ZAND IBAN 迁移 (ZAND Migration)
aliases: []
domain: wallet
status: active
owner: qianlong.wang
reviewer: qianlong.wang
last_reviewed_at: '2026-06-24'
source_type: repo
source_ref: cgs-apitest/testcases/payment
tags: [wallet, cgs-apitest]
related_services: [svc_vis, svc_member, svc_kyc]
related_tables: []
related_logs: []
---

# ZAND IBAN 迁移 (ZAND Migration)

> 业务测试场景。来源 cgs-apitest 回归。

## 场景描述
ZAND 虚拟账户/IBAN 迁移:自动开户(auto_open_zand_iban)、迁移引擎、迁移通知、白名单灰度(whitelist gating)、VAM 查询。经 visii(VA)+ member,KYC 用户白名单触达 kyc。

## 关联关系
- **涉及服务**:[[svc_vis]]、[[svc_member]]、[[svc_kyc]](= `related_services`)
- **覆盖的自动化**:见各 [[auto_*]]
- **读写的表**:待补

## 校验点(QA)
- 白名单灰度命中/未命中分支;自动开户 IBAN 分配(status='V')。
- 迁移引擎幂等与状态;迁移通知触达。
- VAM 查询返回 IBAN/account_type;落库 visii.t_va。

## 来源与置信
- cgs-apitest 套件整理;服务链由调用线索+callgraph 推断,部分待补。
