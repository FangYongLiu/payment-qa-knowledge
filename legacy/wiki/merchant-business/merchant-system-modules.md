---
title: 商户端系统模块与控台清单
domain: merchant-business
kind: wiki_page
slug: merchant-system-modules
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki
source_ref: wiki:da8b5ea6-e2ce-4add-9c83-bb0e520858e5
tags: []
---

# 商户端系统模块与控台清单

本页汇总 Payby 商户端涉及的统一控台、运营后台与各业务模块的功能定位、访问地址与登录信息，便于新同事快速定位入口。相关背景见 [[merchant-business-overview]]。

## 模块总览

Payby 商户端由面向商户的外部控台（Outer Portal）、内部运营后台（Inner Portal）以及围绕收单、出款、POS、WPS 等具体业务的功能模块组成，覆盖入驻、开通、交易、结算、设备与发薪等完整链路。

## 商户统一控台（Unified Portal）

- 定位：商户的统一入口（Outer Portal）
- 功能：
  - 商户登录 / 注册
  - 商户入驻
  - 业务开通（Acquire 或 WPS）
- 访问地址（Sim Env）：`https://sim-web-unified.test2pay.com/verify/login`
- 测试账号：
  - Mobile：`+971-556579167`
  - Password：`132580`
  - Merchant：`SimBasisMerchant0628`

## 业务运营后台（BMOC - Basis Merchant）

- 定位：内部运营后台（Inner Portal）
- 功能：
  - 商户入驻审批
  - 开通支付产品
  - 管理商户信息 / 权限
  - 门店管理
  - 资金渠道报备
  - POS 设备审批
- 访问地址（Sim Env）：`http://sim-admin.corp.test2pay.com/bmoc/`
- 登录方式：
  - Name / Password：员工域账号 / 密码
  - 账号无法登录请联系 OPS：`wei.li`
  - 登录成功后需找 QA 添加角色权限

## 商户收单（Acquire）

- 定位：Online Business
- 说明：商户通过 API 网关、QR、PayLink 发起交易，由系统处理收单行为
- 入口：从统一控台登录，选择 `Payment` 业务

## 商户出款（FundOut）

- 定位：Online Business
- 功能：商户余额提现、转账到 IBAN 或 CardNo
- 入口：从统一控台登录，选择 `Payment` 业务

## POS 业务

- 定位：Offline Business
- 功能：POS 终端的申请、激活、绑定
- 入口：从统一控台登录，选择 `Payment` 业务

## WPS 业务

- 定位：Business
- 功能：为企业提供发薪业务
- 入口：从统一控台登录，选择 `WPS` 业务

## Bank 控台

- 定位：定制化控台（Business）
- 访问地址（Sim Env）：`https://sim-cooperation.test2pay.com/`
- 测试账号：
  - Account：`can.wang@payby.com`
  - Pwd：`1qaz!QAZ`

## 环境与登录提示

- 上述地址均为 Sim 环境（测试环境），用于 QA 验证。
- 外部控台（统一控台、Bank 控台）使用商户/业务账号登录；内部控台（BMOC）使用员工域账号登录，并需额外配置角色权限。

> 所属业务域：[[domain_merchant_business]]
