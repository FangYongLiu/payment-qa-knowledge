---
title: Payby商户端系统模块与控台清单
domain: merchant-business
kind: wiki_page
slug: merchant-business-modules
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:AQ/997818451
tags: []
---

# Payby商户端系统模块与控台清单

本页汇总 Payby 商户端涉及的各控台与业务模块，包括统一控台、BMOC、收单、出款、POS、WPS 及 Bank 控台的功能定位、访问地址与登录信息，便于新同事快速上手。整体业务背景见 [[merchant-business-overview]]。

## 商户统一控台 (Unified Portal)

- **功能**：商户登录/注册、商户入驻、业务开通（Acquire 或 WPS）
- **类型**：Outer Portal
- **Sim 访问地址**：https://sim-web-unified.test2pay.com/verify/login
- **测试账号**：
  - Mobile：+971-556579167
  - Password：132580
  - Merchant：SimBasisMerchant0628

## 业务运营后台 (BMOC - Basis Merchant)

- **功能**：
  - 商户入驻审批
  - 开通支付产品
  - 管理商户信息/权限
  - 门店管理
  - 资金渠道报备
  - POS 设备审批
- **类型**：Inner Portal
- **Sim 访问地址**：http://sim-admin.corp.test2pay.com/bmoc/
- **登录方式**：员工域账号/密码
  - 账号无法登录，找 OPS：wei.li
  - 登录成功后需找 QA 添加角色权限

## 商户收单 (Acquire)

- **功能**：商户通过 API 网关、QR、PayLink 发起交易，系统处理收单行为
- **类型**：Online Business
- **入口**：从统一控台登录，选择 `Payment` 业务

## 商户出款 (FundOut)

- **功能**：商户余额提现、转账到 IBAN 或 CardNo
- **类型**：Online Business
- **入口**：从统一控台登录，选择 `Payment` 业务

## POS 业务

- **功能**：POS 终端的申请、激活、绑定
- **类型**：Offline Business
- **入口**：从统一控台登录，选择 `Payment` 业务

## WPS 业务

- **功能**：为企业提供发薪业务
- **类型**：Business
- **入口**：从统一控台登录，选择 `WPS` 业务

## Bank 控台

- **功能**：定制化控台
- **类型**：Business
- **Sim 访问地址**：https://sim-cooperation.test2pay.com/
- **测试账号**：
  - Account：can.wang@payby.com
  - Pwd：1qaz!QAZ

## 模块速查表

| 模块 | 类型 | 入口/地址 |
|---|---|---|
| 商户统一控台 | Outer Portal | sim-web-unified.test2pay.com |
| BMOC | Inner Portal | sim-admin.corp.test2pay.com/bmoc/ |
| Acquire 收单 | Online | 统一控台 → Payment |
| FundOut 出款 | Online | 统一控台 → Payment |
| POS | Offline | 统一控台 → Payment |
| WPS | Business | 统一控台 → WPS |
| Bank 控台 | Business | sim-cooperation.test2pay.com |

> 所属业务域：[[domain_merchant_business]]
