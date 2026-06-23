---
id: domain_merchant_business
object_type: Domain
domain: merchant-business
status: archived
owner: wiki-sync@acquire
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-19'
source_type: wiki
source_ref: confluence:AQ/997818451
tags:
- merchant
- acquire
- fundout
- pos
- wps
subdomain: null
module: null
sensitivity: normal
name: 商户业务域
aliases: []
related_services: []
related_tables: []
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 概述
Payby 商户业务域是支付体系中的核心部分，面向各类企业商户（线上电商平台、线下零售店、收银系统集成商等），提供交易收款、账单管理、账户管理、POS设备接入与出款结算等完整能力。

## 覆盖范围
- 商户入驻与注册（统一控台 Outer Portal）
- 业务开通：Acquire（收单）、WPS（发薪）
- 商户入驻审批、支付产品开通、商户信息/权限管理、门店管理、资金渠道报备、POS设备审批（BMOC 业务运营后台）
- 商户收单 Acquire：通过 API网关、QR、PayLink 发起交易
- 商户出款 FundOut：余额提现、转账到 IBAN 或 CardNo
- POS 业务：POS 终端的申请、激活、绑定
- WPS 业务：为企业提供发薪业务
- Bank 控台：定制化控台

## 关键服务/流程
- 商户统一控台 (Unified Portal)：商户登录/注册、入驻、业务开通（Acquire / WPS）
  - 访问地址（Sim）：https://sim-web-unified.test2pay.com/verify/login
  - 测试样例：Merchant=SimBasisMerchant0628，Mobile=+971-556579167，Password=132580
- 业务运营后台 (BMOC - Basis Merchant)：商户入驻审批、开通支付产品、管理商户信息/权限、门店管理、资金渠道报备、POS设备审批
  - 访问地址（Sim）：http://sim-admin.corp.test2pay.com/bmoc/
  - 登录账号：员工域账号/密码（账号问题联系 OPS: wei.li），登录成功后由 QA 添加角色权限
- 商户收单 (Acquire)：从统一控台登录，选择 'Payment' 业务（Online Business）
- 商户出款 (FundOut)：从统一控台登录，选择 'Payment' 业务（Online Business）
- POS 业务：从统一控台登录，选择 'Payment' 业务（Offline Business）
- WPS 业务：从统一控台登录，选择 'WPS' 业务
- Bank 控台：定制化控台，访问地址（Sim）：https://sim-cooperation.test2pay.com/
  - 测试账号：can.wang@payby.com / 1qaz!QAZ

## QA 关注点
- 区分 Outer Portal（商户侧统一控台）与 Inner Portal（BMOC 运营后台）的入口与权限模型
- BMOC 登录需员工域账号，并由 QA 协助添加角色权限后才能完成相应审批/管理操作
- Acquire 与 FundOut 均从统一控台 'Payment' 业务进入，需区分 Online 与 Offline 场景（POS 属 Offline Business）
- WPS 与 Payment 是并列的业务入口，需在统一控台选择对应业务
- Bank 控台为定制化控台，账号体系独立（示例账号：can.wang@payby.com）
- 测试样例商户：SimBasisMerchant0628（Mobile:+971-556579167）
