---
title: Merchant Portal 商户入驻流程
domain: payby-authorization-protocol
kind: wiki_page
slug: payby-merchant-portal-onboarding-flow
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:8882b824-31e1-4321-8b26-e3eb71221d87
tags: []
---

# Merchant Portal 商户入驻流程

本页描述商户在 Merchant Portal（商户控台）完成注册、入驻申请、审核与账户激活的端到端时序流程。

## 参与方

- Enterprise Operator（企业操作员）
- Unified Portal（统一控台）
- Member Service（会员服务）
- Merchant System（商户系统）
- Basis（运营审核）
- AML（反洗钱检查）
- VIS（商户信息同步目标系统）
- Billing System（计费系统）
- Contract System（合约系统）

## 时序流程

1. Enterprise Operator → Unified Portal：Register / Login (Mobile Number)
2. Unified Portal → Member Service：Create Member Account
3. Member Service → Unified Portal：Member ID Created
4. Enterprise Operator → Unified Portal：Submit Merchant Onboarding Information
5. Unified Portal → Merchant System：Create Merchant Application
6. Merchant System → Merchant System（自调用）：Create Review Order
7. Merchant System → Basis：Submit for Operational Review
8. Basis → Merchant System：Review Decision (Approve / Reject)
9. Merchant System → AML：Submit Merchant Info for AML Check
10. AML → Merchant System：AML Result
11. Merchant System → Member Service：Activate Corporate Member Account
12. Member Service → Merchant System：Account Activated
13. Merchant System → VIS：Sync Merchant Information
14. VIS → Merchant System：Sync Result

## 关键阶段说明

- **注册登录**：通过 Mobile Number 在 Unified Portal 完成注册/登录，由 Member Service 创建并返回 Member ID。
- **入驻申请**：操作员提交商户入驻信息后，Unified Portal 调用 Merchant System 创建 Merchant Application，并在内部生成 Review Order。
- **审核环节**：先经 Basis 进行运营审核（Approve / Reject），通过后再交由 AML 进行反洗钱检查。
- **账户激活**：审核与 AML 通过后，由 Merchant System 通知 Member Service 激活 Corporate Member Account（企业会员账户）。
- **信息同步**：激活后 Merchant System 将商户信息同步至 VIS，并接收同步结果。

## 备注

- Billing System 与 Contract System 作为参与方出现在图示中，但在本流程的消息序列中未触发显式交互。
