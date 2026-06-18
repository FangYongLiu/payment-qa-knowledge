---
id: domain_merchant_business
object_type: Domain
domain: merchant-business
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: wiki
source_ref: confluence:AQ/997818451
tags:
- 商户
- 收单
- 出款
- POS
- WPS
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
商户业务域是 Payby 支付体系中的核心部分，面向各类企业商户（如线上电商平台、线下零售店、收银系统集成商等），提供交易收款、账单管理、账户管理、POS设备接入与出款结算等完整能力。

## 覆盖范围
- 商户入驻、登录/注册、业务开通（Acquire / WPS）
- 商户信息与权限管理、门店管理、资金渠道报备、POS设备审批
- 商户收单（Acquire）：通过 API 网关、QR、PayLink 发起交易及收单处理
- 商户出款（FundOut）：商户余额提现、转账到 IBAN 或 CardNo
- POS 业务：POS 终端的申请、激活、绑定（Offline Business）
- WPS 业务：为企业提供发薪业务
- Bank 控台：定制化控台

## 关键服务/流程
- 商户统一控台（Unified Portal）：商户登录/注册、入驻、业务开通入口
- 业务运营后台（BMOC - Basis Merchant）：内部运营审批与管理（入驻审批、支付产品开通、商户信息/权限、门店、资金渠道报备、POS 审批）
- 商户收单（Acquire）：从统一控台登录后选择 'Payment' 业务进入（Online Business）
- 商户出款（FundOut）：从统一控台登录后选择 'Payment' 业务进入（Online Business）
- POS 业务：从统一控台登录后选择 'Payment' 业务进入（Offline Business）
- WPS 业务：从统一控台登录后选择 'WPS' 业务进入
- Bank 控台：定制化业务控台（sim-cooperation 环境）

## QA 关注点
- 商户全生命周期：入驻 → 审批（BMOC） → 业务开通（Acquire / WPS） → 交易/出款/POS/WPS 操作
- Outer Portal（商户侧）与 Inner Portal（运营侧 BMOC）的功能边界与权限联动
- 收单（API 网关 / QR / PayLink）多入口的交易链路
- 出款渠道差异：余额提现、IBAN 转账、CardNo 转账
- POS 终端：申请、激活、绑定流程及审批闭环
- WPS 发薪业务的独立业务入口
- BMOC 登录依赖员工域账号，需 QA 配合分配角色权限
