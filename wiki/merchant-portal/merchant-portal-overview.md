---
title: Merchant Portal 商户控台总览
domain: merchant-portal
kind: wiki_page
slug: merchant-portal-overview
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki
source_ref: wiki:fa5361b9-9768-4302-b8dc-f2dd9cc50451
tags: []
---

# Merchant Portal 商户控台总览

Merchant Portal 是商户进入系统的统一前端入口，承担商户注册/登录、业务类型申请（Payment 或 WPS）以及商户后台管理（交易订单、账户、对账单、支付产品、线下设备、设置）等功能。

## 核心功能

- 商户注册与登录入口
- 业务类型申请：Payment（即收单 Acquire 服务）或 WPS
- 商户管理后台：transaction Order / Account / Statement / Payment Products / Offline Device / Setting

## 环境与测试账号

| 环境 | 访问地址 | 登录信息 |
|------|----------|----------|
| Sim | https://sim-web-unified.test2pay.com/verify/login | Mobile: +971-556579167；Password: `132580` 或 `Yong0324####`；OTP: `161616`（默认）；Choose Merchant: `SimBasisMerchant0628` |
| Uat | https://uat-web-unified.test2pay.com/verify/login | Mobile: +971-556579167；Password: `132580` 或 `Yong0324####`；OTP: real OTP |

说明：
- 首次注册默认通过 OTP 登录，登录后必须设置密码。
- Sim 默认 OTP 固定为 `161616`；Uat 必须使用真实 OTP。

## 业务流程图（跨系统联动）

商户 onboarding 是一个跨系统的流程，**只有所有服务都成功完成，商户才可用**。涉及的服务及职责如下：

| Service | 职责说明 |
|---------|----------|
| Member | 全系统统一身份服务，管理个人/企业 Member 账户，向下游提供 Member ID |
| Merchant | 商户域服务，负责商户档案、onboarding 状态、商户–Member 关系、商户生命周期 |
| Basis | 核心基础服务，处理账户启用、产品激活、运营审核、内部核心配置 |
| AML | 反洗钱合规与风险筛查；AML 失败会阻断商户激活 |
| VIS | 虚拟 IBAN 服务，负责虚拟 IBAN 账户创建与外部对接 |
| Billing | 计费与账务服务，负责 billing 账户创建、订单初始化、结算配置 |
| Contract | 合同管理服务，onboarding 成功后生成并管理商户合同 |
| Unified Portal | 商户注册与 onboarding 提交的前端入口 |

详细 onboarding 端到端流程见 [[merchant-onboarding-flow]] 与 [[flow_merchant_onboarding]]。

## 主要业务模块

- **商户注册 / 登录**：首次注册走 OTP 登录，之后强制设置密码。
- **商户 Onboarding**：填写 onboarding 表单，含 Company Bank Account（如 IBAN `AE790030013112189920001`，由后端服务校验）。
- **业务类型选择**：选择 Company Business Type = `Payment` 即开通收单（Merchant Acquire Service）。
- **管理员信息**：填写的 Mobile number 即为登录手机号，并具有 administrator 角色。
- **状态审批（BMOC 审核）**：登录 BMOC（Basis Merchant => Business => Merchant => Merchant Onboarding），依次完成 AML Risk Calculate 与 KYB Approval，再回查商户状态。

收单商户控台（Acquire Merchant Console）下的支付产品申请、交易、账户、对账单、线下业务、商户设置等详见 [[acquire-merchant-console]]，相关测试场景见 [[scn_acquire_product_apply]]。

## 数据库与基础设施

- Onboarding 影响的数据库与表清单：见 [[merchant-onboarding-database-scope]]
- DB / Redis / Kibana 连接方式与 QA 账号权限：见 [[qa-infra-access-guide]]

## 服务与组件

- 服务组件清单与各 Owner：见 [[merchant-portal-service-components]]

## 文档目的

- 介绍商户注册流程
- 明确测试重点，包括数据库检查与 BMOC 审核依赖
