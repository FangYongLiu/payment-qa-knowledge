---
id: flow_merchant_portal_onboarding
object_type: Flow
domain: authorization-protocol
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: wiki_image
source_ref: wiki_image:23a2b805-1739-48ca-bf4e-31c68c317038
tags:
- merchant-onboarding
- merchant-portal
- sequence
subdomain: merchant-portal
module: null
sensitivity: normal
name: 商户控台商户入驻端到端流程
aliases: []
related_services: []
related_tables: []
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 概述
描述企业操作员（Enterprise Operator）通过 Unified Portal 完成商户入驻的端到端时序流程。流程跨越 Member Service、Merchant System、Basis、AML、VIS、Billing System 等系统，覆盖会员注册、商户申请提交、运营审核、AML 检查、企业会员激活、商户信息同步与计费账户创建。

## 步骤(跨系统)
1. Enterprise Operator → Unified Portal：Register / Login (Mobile Number)
2. Unified Portal → Member Service：Create Member Account
3. Member Service ⇠ Unified Portal（返回）：Member ID Created
4. Enterprise Operator → Unified Portal：Submit Merchant Onboarding Information
5. Unified Portal → Merchant System：Create Merchant Application
6. Merchant System → Merchant System（自调用）：Create Review Order
7. Merchant System → Basis：Submit for Operational Review
8. Basis ⇠ Merchant System（返回）：Review Decision (Approve / Reject)
9. Merchant System → AML：Submit Merchant Info for AML Check
10. AML ⇠ Merchant System（返回）：AML Result
11. Merchant System → Member Service：Activate Corporate Member Account
12. Member Service ⇠ Merchant System（返回）：Account Activated
13. Merchant System → VIS：Sync Merchant Information
14. VIS ⇠ Merchant System（返回）：Sync Result
15. Merchant System → Billing System：Create Billing Account
16. Billing System ⇠ Merchant System（返回）：Billing Account Created

## 涉及服务/表
- Unified Portal：商户控台入口，承载注册/登录与商户入驻信息提交
- Member Service：创建个人会员账户、激活企业会员账户（Corporate Member Account）
- Merchant System：创建 Merchant Application、生成 Review Order，编排后续审核与同步
- Basis：执行运营审核（Operational Review），返回 Approve / Reject
- AML：对商户信息执行 AML Check，返回 AML Result
- VIS：商户信息同步
- Billing System：创建商户计费账户

## 校验点
- 注册/登录使用手机号（Mobile Number），需返回 Member ID Created
- Merchant Application 创建后必须生成 Review Order
- Basis 运营审核需返回 Approve 或 Reject 决策
- AML Check 需返回 AML Result，决定后续激活流程是否继续
- 企业会员账户需在 Member Service 完成 Activate（Account Activated）
- 商户信息需通过 VIS 同步并返回 Sync Result
- Billing System 必须返回 Billing Account Created，入驻流程方告完成
