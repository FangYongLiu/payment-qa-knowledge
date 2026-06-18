---
title: 商户注册与Onboarding流程
domain: merchant-portal
kind: wiki_page
slug: merchant-onboarding-flow
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki
source_ref: wiki:fa5361b9-9768-4302-b8dc-f2dd9cc50451
tags: []
---

# 商户注册与Onboarding流程

本页描述商户从 Unified Portal 注册登录、填写 Onboarding 表单、选择业务类型，到 BMOC 后台完成 AML + KYB 审核的端到端流程。完整端到端串联见 [[flow_merchant_onboarding]]，落库范围见 [[merchant-onboarding-database-scope]]，相关服务清单见 [[merchant-portal-service-components]]。

## 流程概览

商户 Onboarding 是一个跨系统流程，只有所有服务全部成功后，商户才真正可用。涉及的核心服务及职责：

- **Unified Portal**：商户注册与 Onboarding 提交的前端入口。
- **Member**：全系统的中心用户身份服务，管理个人/企业会员账户，提供 Member ID 给下游服务。
- **Merchant**：商户域服务，负责商户档案、Onboarding 状态、商户–会员关系、商户生命周期。
- **Basis**：核心基础服务，负责账户启用、产品激活、运营审核决策、内部核心配置。
- **AML**：反洗钱合规与风险筛查；AML 不通过将阻断商户激活。
- **VIS**：虚拟 IBAN 账户的创建与外部对接。
- **Billing**：账单/记账，负责计费账户创建、订单初始化、结算配置。
- **Contract**：Onboarding 成功后生成并管理商户合同。

## 入口环境与测试账号

Merchant Portal 总览见 [[merchant-portal-overview]]。

| 环境 | 访问地址 |
|---|---|
| Sim | https://sim-web-unified.test2pay.com/verify/login |
| Uat | https://uat-web-unified.test2pay.com/verify/login |

测试账号：
- Mobile：`+971-556579167`
- Password：`132580` 或 `Yong0324####`
- OTP：Sim 默认 `161616`；Uat 需要 **real OTP**
- Choose Merchant（Sim）：`SimBasisMerchant0628`

## 商户注册 / 登录

- 首次注册默认通过 **OTP 登录**，登录后必须设置密码。
- Sim 环境 OTP 默认值固定为 `161616`；Uat 必须使用真实 OTP。

## Onboarding 表单填写

在 Unified Portal 填写 Onboarding 表单。

- **Company Bank Account / IBAN**：测试值 `AE790030013112189920001`（该字段由后端服务校验）。

## 业务类型选择（Business Type）

- **Company Business Type** 选择 `Payment`，即 Merchant Acquire Service（收单服务）。后续即可进入 [[acquire-merchant-console]]，并可参考 [[scn_acquire_product_apply]] 验证产品申请。
- **Administrator Information / Mobile number**：
  - 注册成功后使用 **该手机号** 登录 Portal。
  - 该手机号天然带有 **administrator** 角色。

## BMOC 审核（AML + KYB）

商户提交后需进入 BMOC 后台完成审核。

- 登录入口：`https://sim-admin.corp.test2pay.com/basis-cas/login?service=https://sim-admin.corp.test2pay.com/bmoc/cas`
- 菜单路径：**Basis Merchant => Business => Merchant => Merchant Onboarding**

审核步骤：

1. **Step 1**：完成 **AML Risk Calculate**（AML 风险测算）。
2. **Step 2**：完成 **KYB Approval**（KYB 审核）。
3. 系统处理结束后，回到列表查看商户状态确认是否激活成功。

> AML 任意校验失败将阻断商户激活；只有 Member / Merchant / Basis / AML / VIS / Billing / Contract 等下游均成功，商户才转为可用状态。

## 测试要点

- 注册登录链路：OTP 下发与登录、首次登录强制设密、管理员手机号绑定。
- 表单校验：IBAN 等字段由后端服务校验，需用合法测试值。
- 业务类型：`Payment` 链路触发收单相关服务初始化。
- BMOC 审核两步必须依次完成（AML → KYB），缺一不可。
- 审核完成后核对商户状态，并按 [[merchant-onboarding-database-scope]] 中表与字段进行落库校验；DB / Redis / Kibana 访问见 [[qa-infra-access-guide]]。
