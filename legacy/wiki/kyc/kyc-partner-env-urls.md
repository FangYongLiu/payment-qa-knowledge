---
title: KYC各业务方环境URL配置
domain: kyc
kind: wiki_page
slug: kyc-partner-env-urls
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki
source_ref: wiki:c77c6bdf-23d4-4c31-b325-128a8f8a6d3e
tags: []
---

# KYC各业务方环境URL配置

本页汇总 CashNow、Botim、PayBy 三个业务方在 SIM/UAT/PROD 环境下，KYC 入口、活体核身入口、回调（redirect）地址以及 Contact Us 链接的完整清单，供前后端及业务方接入时查阅。相关接口协议见 [[eid-kyc-cgs-api-v2-overview]]。

## CGS Domain（CGS API 接入域名）

- SIM: `https://sim.test2pay.com/cgs/api`
- UAT: （同上一份配置环境域名）
- PROD: （生产环境域名）

> 业务侧调用 [[api_kyc_eid_start_journey]]、[[api_kyc_body_auth_apply]] 等 CGS 接口时使用上述 Domain；返回的 `videoUrl` / `nextStep` 会指向下文各业务方的 Web/MP 入口。

## CashNow

### KYC 入口
- SIM/UAT `cashnow-kyc-applyurl`: `https://uat-identity.test2pay.com/kyc/home?pbw_show_title=N&partner=cashnow`
- PROD `cashnow-kyc-applyurl`: `https://identity.botim.money/kyc/home?pbw_show_title=N&partner=cashnow`

### KYC 回调（redirect）
- SIM/UAT `cashnow-kyc-redirecturl`: `https://uat-identity.test2pay.com/broadcast.html`
- PROD `cashnow-kyc-redirecturl`: `https://identity.botim.money/broadcast.html`

### Contact Us
- SIM/UAT `cashnow-kyc-contactUs`: `https://uat.test2pay.com/creditforvip/?pbw_show_title=N#/contactUs?from=signzy`
- PROD `cashnow-kyc-contactUs`: `https://m.cashnow.ai/creditforvip/?pbw_show_title=N#/contactUs?from=signzy`

### 活体核身（申请态 / 登录态共用同一 URL）
- SIM/UAT `cashnow-liveness-applyurl`: `https://uat-identity.test2pay.com/biometric?pbw_show_title=N&partner=cashnow`
- PROD `cashnow-liveness-applyurl`: `https://identity.botim.money/biometric?pbw_show_title=N&partner=cashnow`
- 回调地址复用 `cashnow-kyc-redirecturl`（同上）

## Botim

### MP KYC 入口
- SIM/UAT & PROD `botim-pay-KYC-applyurl`: `https://botim.me/mp/b/?app=me.botim.pay.kyc`

### MP / Web 回调（redirect）
- MP `botim-pay-redirecturl`（SIM/UAT & PROD）: `https://me.botim.pay.security/broadcast.html`
- Web `botim-pay-redirecturl`:
  - SIM/UAT: `https://uat-identity.test2pay.com/broadcast.html`
  - PROD: `https://identity.botim.money/broadcast.html`

### MP 活体核身入口（申请态）
- SIM/UAT & PROD `botim-pay-liveness-applyurl`:
  `https://botim.me/mp/b/?app=me.botim.pay.security%2Findex.html%2F%23%2Fbiometric%3Fsignzy_url%3D%24%7Bsignzy_url%7D`
- 占位符 `${signzy_url}` 由后端用 signzy 链接做 URL encode 后拼入。

### Web 活体核身入口（申请态）
- SIM/UAT `botim-pay-liveness-applyurl`: `https://uat-identity.test2pay.com/biometric?pbw_show_title=N&partner=botim`
- PROD `botim-pay-liveness-applyurl`: `https://identity.botim.money/biometric?pbw_show_title=N&partner=botim`

> Web KYC 入口未单独列出，使用通用 identity 域下的 `/kyc/home` 路径（参考 CashNow/PayBy 形态，partner 替换为 `botim`）。

## PayBy

### KYC 入口
- SIM/UAT `payby-KYC-applyurl`: `https://uat-identity.test2pay.com/kyc/home?pbw_show_title=N&partner=payby`
- PROD `payby-KYC-applyurl`: `https://identity.botim.money/kyc/home?pbw_show_title=N&partner=payby`

### KYC / 活体 回调（redirect，复用同一地址）
- SIM/UAT `payby-redirecturl`: `https://uat-identity.test2pay.com/broadcast.html`
- PROD `payby-redirecturl`: `https://identity.botim.money/broadcast.html`

### Contact Us
- UAT `payby-contactUs`: `https://uat-m.test2pay.com/platform/payby/faqs/helpCenter`
- PROD `payby-contactUs`: `https://m.payby.com/platform/payby/faqs/helpCenter`

### 活体核身（申请态 / 登录态共用同一 URL）
- SIM/UAT `payby-liveness-applyurl`: `https://uat-identity.test2pay.com/biometric?pbw_show_title=N&partner=payby`
- PROD `payby-liveness-applyurl`: `https://identity.botim.money/biometric?pbw_show_title=N&partner=payby`

## URL 拼装与使用约定

- KYC 入口与活体入口均通过查询参数 `partner=<cashnow|botim|payby>` 区分业务方，`pbw_show_title=N` 控制隐藏标题栏。
- `redirectUrl`（回调）由调用方在 [[api_kyc_eid_start_journey]] / [[api_kyc_body_auth_apply]] / [[api_kyc_body_unauth_apply]] / [[api_kyc_eid_retake_selfie]] 请求中传入；KYC 完成后页面会跳转到对应 `broadcast.html`。
- 活体接口 v2（[[api_kyc_body_auth_apply]] 的 `/kyc/body-auth/v2/liveness/apply`）返回的 `videoUrl` 由 config repo 中的 `applyUrlV2`（即上述 `*-liveness-applyurl`）拼接 signzy URL 组成。
- v1 活体接口的 HTTP 模式 `videoUrl` 形如 `<MP小程序地址>/?url=<signzy url>`，其中 signzy url 需由后端做 `encodeUrl`。
- 三方业务域整体说明见 [[domain_kyc]]。
