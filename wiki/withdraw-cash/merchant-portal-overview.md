---
title: Merchant Portal 商户控台总览
domain: withdraw-cash
kind: wiki_page
slug: merchant-portal-overview
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:23c98c4c-4437-474a-9c1b-42697ceba59d
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

## Withdraw 提现流程（移动端）

Merchant Portal 移动端提供 Withdraw money 提现入口，主要要素：

- **Withdraw money 页面**：
  - 顶部展示可用余额，例如 `Balance: 865.62 AED`（带 info 图标）
  - 金额输入框（dirham 前缀），支持快捷金额按钮（如 `500`）和 `Max`
  - `View limit` 链接查看额度
  - `Choose your withdrawal method`：方法卡片展示渠道、到账时效与手续费，例如：
    - `Aani`（标记 `Recommended`），`Instant` 到账，手续费 `AED 0.50`
- **Withdrawal 确认弹窗（bottom sheet）**：
  - 顶部展示总扣款金额，例如 `AED 502.00`（含手续费）
  - 副标题 `Withdraw money`
  - 账户选择卡：银行名称（如 `WIO BANK P.J.S.C.`）、脱敏账号（如 `******************0327`）、右侧 `Change` 可切换
  - 主 CTA：`Withdraw` 按钮提交提现

## BMOC 审核入口

入驻后由业务运营在 BMOC 完成审核：

- 登录：`https://sim-admin.corp.test2pay.com/basis-cas/login?service=https://sim-admin.corp.test2pay.com/bmoc/cas`
- 菜单：`Basis Merchant => Business => Merchant => Merchant Onboarding`
- 步骤：
  1. 完成 AML Risk Calculate
  2. 完成 KYB Approval

## 文档导航

- 注册与入驻全流程：[[merchant-onboarding-flow]]
- 入驻所涉服务/组件与 Owner：[[merchant-onboarding-service-map]]
- 入驻影响的数据库与表：[[merchant-onboarding-database-scope]]
- 收单商户控台（Acquire Merchant Console）使用：[[acquire-merchant-console-guide]]
- 收单产品申请与审核流程：[[flow_acquire_product_application]]
- 数据库 / Redis / Kibana 等基础设施访问：[[merchant-portal-env-access-guide]]
