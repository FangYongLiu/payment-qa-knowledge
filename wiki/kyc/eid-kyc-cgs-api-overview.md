---
title: EID KYC CGS API 总览
domain: kyc
kind: wiki_page
slug: eid-kyc-cgs-api-overview
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:PMDPayment/1089405294
tags: []
related_services:
  - svc_cgs
  - svc_kyc
---

# EID KYC CGS API 总览

本页汇总 EID KYC CGS API V2 的接口分组、域名与调用规范，作为 [[domain_kyc]] 业务域下 KYC 全流程对接的入口索引。

## 域名与环境

- 基础路径：`{host}/cgs/api`
- SIM：`https://sim.test2pay.com/cgs/api`
- UAT / PROD：详见 [[eid-kyc-environment-urls]]
- 各业务方（Botim / PayBy / CashNow）的 KYC、Liveness、回调、Contact Us URL 配置，参见 [[eid-kyc-environment-urls]]

## 调用规范

- 所有接口请求与响应 Body 均为 JSON。
- HTTP Method：均为 `POST`。
- 成功标识：`status=200` 表示成功。
- 通用响应字段：
  - `commandType`：`tips`（展示提示）/ `moveForward`（前进到下一步）/ `action`（执行动作，部分接口）。
  - `commandData`：根据 `commandType` 返回 `TipsInfo` 或下一步路由 / 数据。
- 敏感信息加密：`name`、`idNumber` 等需通过 RSA 加密后传输；VIP 场景下接口返回会以 `*` 脱敏展示。

## 路由约定（nextStep）

`commandData.nextStep` 可能为：
- 外部 URL（如 signzy 链接，配合 `mode=HTTP`）
- TOKEN（`mode=TOKEN`）
- 原生路由：`route://native/kyc/result`、`route://native/kyc/re-submit`
- 站内路径：`/kyc/home`、`/kyc/choose-account` 等

## 接口分组

### 1. EID KYC Flow（`/kyc/active-account/v1/...`）

KYC 主流程，覆盖状态查询、旅程启动、结果获取、信息确认/编辑、重试与放弃。

- [[api_kyc_check_reminder]]：`/kyc/check-reminder`，检查 KYC 状态并提醒用户尽快完成确认。
- [[api_kyc_inquire_info]]：`/kyc/inquire-info`，查询用户 KYC 信息（含 `kycStatus`：NON / PROCESS / FINISH / EXPIRED / BLOCKED / RESUBDOC / AUDIT）。
- [[api_kyc_eid_start_journey]]：`/eid/main/start-journey`，创建/获取 KYC 旅程链接。
- [[api_kyc_eid_get_result]]：`/eid/main/get-result`，获取 KYC 旅程结果，驱动结果页展示。
- [[api_kyc_eid_inquire_industry]]：`/eid/inquire-industry`，获取行业列表供用户选择。
- [[api_kyc_eid_confirm_info]]：`/eid/main/confirm-info`，用户确认 EID 信息（不进入人工审核）。
- [[api_kyc_eid_submit_edit]]：`/eid/main/submit-edit`，提交修改后的 EID 信息（进入人工审核）。
- [[api_kyc_eid_retake_selfie]]：`/eid/main/retake-selfie`，活体失败后重新自拍。
- [[api_kyc_eid_get_retake_selfie_result]]：`/eid/main/get-retake-selfie-result`，获取重新自拍结果。
- [[api_kyc_eid_leave_submit]]：`/eid/main/leave-submit`，记录用户放弃 KYC 的原因，不可重新提交。
- [[api_kyc_eid_verify_again]]：`/eid/main/verify-again`，OCR 信息有误时发起新的旅程。

### 2. Body Auth（`/kyc/body-auth/...` 与 `/kyc/body-unauth/...`）

为业务功能提供活体核身能力。

- [[api_kyc_body_auth_apply]]：`/kyc/body-auth/v1/liveness/apply` 与 `v2/liveness/apply`，已认证用户活体申请；V2 的 `videoUrl` 由 config repo 中 `applyUrlV2` 拼接 signzy URL。
- [[api_kyc_body_unauth_apply]]：`/kyc/body-unauth/v1/liveness/apply`，未认证用户活体申请，请求需传加密的 `mobile`。
- 核身验证方式 `model`：`SDK`（Yitu SDK）/ `HTTP`（Webview video url）。

## 整体流程概述

1. 通过 [[api_kyc_check_reminder]] 与 [[api_kyc_inquire_info]] 判断用户是否需要进入或继续 KYC。
2. 调用 [[api_kyc_eid_start_journey]] 启动旅程；若需要活体核身则进入 Body Auth 流程。
3. 用户在 signzy 完成 OCR + Liveness 后，调用 [[api_kyc_eid_get_result]] 获取结果，根据 `commandType/commandData` 跳转至：结果页 / 重新提交 / 重新自拍 / 提示页。
4. 信息无误：调用 [[api_kyc_eid_inquire_industry]] 选行业 → [[api_kyc_eid_confirm_info]] 直接确认。
5. 信息需修改：经 [[api_kyc_eid_submit_edit]] 提交后进入人工审核；OCR 严重错误时使用 [[api_kyc_eid_verify_again]] 重启旅程。
6. 活体失败：使用 [[api_kyc_eid_retake_selfie]] + [[api_kyc_eid_get_retake_selfie_result]] 重试。
7. 用户放弃：调用 [[api_kyc_eid_leave_submit]] 记录原因，禁止再次提交。
