---
title: Merchant Portal 商户入驻流程
domain: authorization-protocol
kind: wiki_page
slug: merchant-portal-onboarding-flow
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:23a2b805-1739-48ca-bf4e-31c68c317038
tags: []
---

# Merchant Portal 商户入驻流程

本页描述企业操作员通过商户控台完成注册登录、提交商户信息、风控审核到账户激活的端到端时序。完整泳道图见 [[flow_merchant_portal_onboarding]]。

## 参与方

- Enterprise Operator：企业操作员
- Unified Portal：统一控台入口
- Member Service：会员服务
- Merchant System：商户系统
- Basis：运营审核
- AML：反洗钱审核
- VIS：商户信息同步目标系统
- Billing System：计费系统
- Contract System：合同系统

## 入驻时序

### 1. 注册登录与会员创建

1. Enterprise Operator → Unified Portal：Register / Login (Mobile Number)
2. Unified Portal → Member Service：Create Member Account
3. Member Service ⇠ Unified Portal：Member ID Created

### 2. 提交商户入驻信息

4. Enterprise Operator → Unified Portal：Submit Merchant Onboarding Information
5. Unified Portal → Merchant System：Create Merchant Application
6. Merchant System → Merchant System：Create Review Order（自环，生成审核单）

### 3. 运营审核与 AML 审核

7. Merchant System → Basis：Submit for Operational Review
8. Basis ⇠ Merchant System：Review Decision (Approve / Reject)
9. Merchant System → AML：Submit Merchant Info for AML Check
10. AML ⇠ Merchant System：AML Result

### 4. 账户激活与下游同步

11. Merchant System → Member Service：Activate Corporate Member Account
12. Member Service ⇠ Merchant System：Account Activated
13. Merchant System → VIS：Sync Merchant Information
14. VIS ⇠ Merchant System：Sync Result
15. Merchant System → Billing System：Create Billing Account
16. Billing System ⇠ Merchant System：Billing Account Created

## 备注

- 入口为 Unified Portal，注册/登录采用手机号方式。
- 商户审核分为两段：Basis 运营审核（Approve / Reject）与 AML 反洗钱审核，两段均通过后才进入账户激活与同步阶段。
- 激活成功后依次完成 VIS 信息同步与 Billing 计费账户创建。
- 图中列出的 Contract System 在该时序的消息序列中未出现交互。
