---
title: Merchant Portal 商户控台总览
domain: withdraw-cash
kind: wiki_page
slug: merchant-portal-overview
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:54f798f3-03f7-4605-a0d3-af90fc11815d
tags: []
---

# Merchant Portal 商户控台总览

Merchant Portal 是商户体系的统一入口，承载商户注册/登录、业务类型申请（Payment 或 WPS）以及商户后台管理（交易订单、账户、对账单、支付产品、线下设备、设置等）。

## 功能定位

- 商户注册/登录入口
- 业务类型申请（Payment 即 Merchant Acquire Service，或 WPS）
- 商户管理后台：
  - 交易订单（transaction Order）
  - 账户（Account）
  - 对账单（Statement）
  - 支付产品（Payment Products）
  - 线下设备（Offline Device）
  - 设置（Setting）

## 环境地址与测试账号

| 环境 | 访问地址 |
| --- | --- |
| Sim | https://sim-web-unified.test2pay.com/verify/login |
| Uat | https://uat-web-unified.test2pay.com/verify/login |

通用测试账号：

- Mobile：`+971-556579167`
- Password：`132580` 或 `Yong0324####`
- OTP：
  - Sim 默认 `161616`
  - Uat 需使用 real OTP
- Choose Merchant（Sim）：`SimBasisMerchant0628`

首次注册默认使用 **OTP** 登录，登录后必须设置密码。

## 业务流程概览

商户入驻是一个跨系统流程，所有相关服务全部成功后商户才可正式使用。详细端到端步骤见 [[merchant-onboarding-flow]] 与 [[flow_merchant_onboarding]]。

涉及的核心服务一览（详见 [[merchant-onboarding-service-map]]）：

- **Member**：系统级用户身份服务，提供下游使用的 Member ID
- **Merchant**：商户域服务，管理 profile / onboarding 状态 / 商户–会员关系 / 生命周期
- **Basis**：核心基础服务，处理账户启用、产品激活、运营审核等
- **AML**：反洗钱与合规筛查，AML 失败会阻断商户激活
- **VIS**：虚拟 IBAN 账户服务
- **Billing**：计费与账务（账单账户、订单初始化、结算配置）
- **Contract**：商户合同生成与管理
- **Unified Portal**：商户注册与入驻提交的前端入口

## BMOC 审核入口

入驻后由业务运营在 BMOC 完成审核：

- 登录：`https://sim-admin.corp.test2pay.com/basis-cas/login?service=https://sim-admin.corp.test2pay.com/bmoc/cas`
- 菜单：`Basis Merchant => Business => Merchant => Merchant Onboarding`
- 步骤：
  1. 完成 AML Risk Calculate
  2. 完成 KYB Approval

## Withdraw 提现交易详情

Withdraw 流程下的 Transaction Details 页面（移动端）展示一笔已完成的银行账户转账（Transfer to Bank Account），主要字段：

| 字段 | 示例值 | 说明 |
| --- | --- | --- |
| 标题 | Transfer to Bank Account | 交易类型 |
| Amount | AED -2.01 | 总扣款金额（负号表示出款） |
| Status | Transaction Completed | 交易状态 |
| Payment method | Aani | 提现使用的支付通道 |
| Receive Amount | AED 0.01 | 收款方实际到账金额 |
| Fees | AED 2.00 | 手续费 |
| Transfer to | \*\*\* \*\*\* 0865 | 收款银行账号（脱敏） |
| Creation Time | 23/03/2026 15:01 | 交易创建时间 |
| Order number | 131774263665176311 | 订单号 |

金额关系：`Amount = Receive Amount + Fees`（示例中 2.01 = 0.01 + 2.00）。

## 文档导航

- 注册与入驻全流程：[[merchant-onboarding-flow]]
- 入驻所涉服务/组件与 Owner：[[merchant-onboarding-service-map]]
- 入驻影响的数据库与表：[[merchant-onboarding-database-scope]]
- 收单商户控台（Acquire Merchant Console）使用：[[acquire-merchant-console-guide]]
- 收单产品申请与审核流程：[[flow_acquire_product_application]]
- 数据库 / Redis / Kibana 等基础设施访问：[[merchant-portal-env-access-guide]]
