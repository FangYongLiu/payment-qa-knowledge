---
title: EID KYC 各业务方环境URL配置
domain: kyc
kind: wiki_page
slug: eid-kyc-environment-urls
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:PMDPayment/1089405294
tags: []
---

# EID KYC 各业务方环境URL配置

本页汇总 CashNow / Botim / PayBy 三个业务方在 SIM/UAT/PROD 环境下，KYC 入口、活体认证（liveness）入口、回调（redirect）以及联系客服等 URL 的配置清单，供前端、配置中心与联调使用。相关接口契约见 [[eid-kyc-cgs-api-overview]]。

## 通用说明

- 所有 URL 均带 `pbw_show_title=N` 与 `partner=<业务方>` 参数（除 Botim MP 走小程序协议外）。
- `redirecturl` 用作 KYC / 活体完成后的广播回调页（`broadcast.html`）。
- 活体 v2 接口 `/kyc/body-auth/v2/liveness/apply` 的 `videoUrl` 由配置仓库的 `applyUrlV2` 与 signzy url 拼接得到。
- 业务方域名规律：
  - SIM/UAT：`https://uat-identity.test2pay.com`
  - PROD：`https://identity.botim.money`

## CashNow

### KYC 入口
- SIM/UAT `cashnow-kyc-applyurl`：`https://uat-identity.test2pay.com/kyc/home?pbw_show_title=N&partner=cashnow`
- PROD `cashnow-kyc-applyurl`：`https://identity.botim.money/kyc/home?pbw_show_title=N&partner=cashnow`

### KYC 回调
- SIM/UAT `cashnow-kyc-redirecturl`：`https://uat-identity.test2pay.com/broadcast.html`
- PROD `cashnow-kyc-redirecturl`：`https://identity.botim.money/broadcast.html`

### 联系客服
- SIM/UAT `cashnow-kyc-contactUs`：`https://uat.test2pay.com/creditforvip/?pbw_show_title=N#/contactUs?from=signzy`
- PROD `cashnow-kyc-contactUs`：`https://m.cashnow.ai/creditforvip/?pbw_show_title=N#/contactUs?from=signzy`

### 活体认证（申请 / 登录共用同一组 URL）
- SIM/UAT `cashnow-liveness-applyurl`：`https://uat-identity.test2pay.com/biometric?pbw_show_title=N&partner=cashnow`
- PROD `cashnow-liveness-applyurl`：`https://identity.botim.money/biometric?pbw_show_title=N&partner=cashnow`
- 回调 URL 复用 `cashnow-kyc-redirecturl`（同上）。

## Botim

### MP KYC 入口
- SIM/UAT、PROD `botim-pay-KYC-applyurl`：`https://botim.me/mp/b/?app=me.botim.pay.kyc`
- `botim-pay-redirecturl`（SIM/UAT、PROD 一致）：`https://me.botim.pay.security/broadcast.html`

### MP 活体认证
- SIM/UAT、PROD `botim-pay-liveness-applyurl`：
  `https://botim.me/mp/b/?app=me.botim.pay.security%2Findex.html%2F%23%2Fbiometric%3Fsignzy_url%3D%24%7Bsignzy_url%7D`
  - 占位 `${signzy_url}` 由后端在拼接时替换为 signzy url。
- 回调：`https://me.botim.pay.security/broadcast.html`

### Web 活体认证
- SIM/UAT `botim-pay-liveness-applyurl`：`https://uat-identity.test2pay.com/biometric?pbw_show_title=N&partner=botim`
- PROD `botim-pay-liveness-applyurl`：`https://identity.botim.money/biometric?pbw_show_title=N&partner=botim`
- SIM/UAT `botim-pay-redirecturl`：`https://uat-identity.test2pay.com/broadcast.html`
- PROD `botim-pay-redirecturl`：`https://identity.botim.money/broadcast.html`

> Web KYC 入口未在原文给出，按需补充。

## PayBy

### KYC 入口
- SIM/UAT `payby-KYC-applyurl`：`https://uat-identity.test2pay.com/kyc/home?pbw_show_title=N&partner=payby`
- PROD `payby-KYC-applyurl`：`https://identity.botim.money/kyc/home?pbw_show_title=N&partner=payby`

### KYC 回调
- SIM/UAT `payby-redirecturl`：`https://uat-identity.test2pay.com/broadcast.html`
- PROD `payby-redirecturl`：`https://identity.botim.money/broadcast.html`

### 联系客服
- UAT `payby-contactUs`：`https://uat-m.test2pay.com/platform/payby/faqs/helpCenter`
- PROD `payby-contactUs`：`https://m.payby.com/platform/payby/faqs/helpCenter`

### 活体认证（申请）
- SIM/UAT `payby-liveness-applyurl`：`https://uat-identity.test2pay.com/biometric?pbw_show_title=N&partner=payby`
- PROD `payby-liveness-applyurl`：`https://identity.botim.money/biometric?pbw_show_title=N&partner=payby`
- 回调复用 `payby-redirecturl`（同上）。

### 活体认证（登录）
- SIM/UAT `payby-liveness-applyurl`：`https://uat-identity...`（原文截断，按申请同址使用）

## 与接口的对应关系

- KYC `applyurl` 通常是承载 [[api_kyc_eid_start_journey]] 返回 `nextStep` 的 Webview 容器；完成后回到 `redirecturl`，再调用 [[api_kyc_eid_get_result]]。
- 活体 `applyurl` 用于承接 [[api_kyc_body_auth_apply]] / [[api_kyc_body_unauth_apply]] 返回的 `videoUrl`（HTTP 模式）。
- v1 与 v2 活体接口的 URL 拼装区别：v1 使用小程序地址 + signzy url（后端需对 signzy url 做 encodeUrl）；v2 使用配置仓库 `applyUrlV2` + signzy url。
