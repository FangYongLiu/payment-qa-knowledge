---
id: domain_kyc
object_type: Domain
domain: kyc
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-20'
source_type: wiki
source_ref: wiki:c77c6bdf-23d4-4c31-b325-128a8f8a6d3e
tags:
- kyc
- eid
- liveness
- body-auth
subdomain: null
module: null
sensitivity: normal
name: KYC身份验证业务域
aliases: []
related_services: []
related_tables: []
related_scenarios:
- eid-kyc-cgs-api-v2-overview
- kyc-partner-env-urls
related_logs: []
related_requirements: []
related_failures: []
---

## 概述
KYC (Know Your Customer) 是 Botim App 用户在进行任何资金相关交易（top-up、transfer、remittance 等）之前必须完成的身份验证业务域。用户进入 Botim App 后，需先通过 KYC 才能开通资金类功能。KYC 可通过多个渠道（channel）完成，具体走哪个渠道取决于用户持有的证件类型与其选择的验证方式。本业务域同时承担活体核身（Body Auth / Liveness）能力，为各业务功能提供安全保障。

## 覆盖范围
KYC 业务域覆盖以下三个 ACTIVE 渠道：

- **UAEKYC**：基于 Emirates ID (EID)，底层走官方 UAE API，是大多数用户使用的主渠道（primary channel）。EID KYC CGS API V2 即服务于该渠道。
- **UAE Pass**：基于 EID，通过 UAE Pass App 完成；底层 provider 为 UAE Pass（政府数字身份）；面向偏好使用 UAE Pass 验证的用户。
- **Passport**：基于护照（Passport），底层 provider 为 Signzy；面向没有 EID 的 WPS workers。

此外，活体核身（Body Auth）能力服务于 KYC Journey 中的 liveness 步骤、登录场景的 liveness 校验，以及业务功能（如 cashnow 申请、botim-pay 应用等）所需的安全校验。

## 关键服务/流程
### EID KYC Flow（V2 接口集）
- [[api_kyc_check_reminder]] `/kyc/active-account/v1/kyc/check-reminder` — 检查 KYC 状态并提醒用户尽快确认 Eid 信息。
- [[api_kyc_inquire_info]] `/kyc/active-account/v1/kyc/inquire-info` — 查询用户 KYC 信息，覆盖 kycStatus（NON / PROCESS / FINISH / EXPIRED / BLOCKED / RESUBDOC / AUDIT），返回 eidInfo / passportInfo（VIP 字段以 `******` 脱敏）。
- [[api_kyc_eid_start_journey]] `/kyc/active-account/v1/eid/main/start-journey` — 启动 KYC journey，创建 journey url；返回 commandType（tips / moveForward）+ commandData，支持 HTTP 与 TOKEN 模式，以及 result / re-submit 路由。
- [[api_kyc_eid_get_result]] `/kyc/active-account/v1/eid/main/get-result` — 获取 KYC journey 结果，分支包括 liveness fail、kyc process、confirm、reSubmit eid、kyc success、kyc fail、ocr eid 已过期。
- [[api_kyc_eid_inquire_industry]] `/kyc/active-account/v1/eid/inquire-industry` — 查询行业列表，供用户选择 industry。
- [[api_kyc_eid_confirm_info]] `/kyc/active-account/v1/eid/main/confirm-info` — 用户确认 Eid 信息（无修改），不进入人工审核。
- [[api_kyc_eid_submit_edit]] `/kyc/active-account/v1/eid/main/submit-edit` — 用户提交修改后的 Eid 信息（idNumber、name 为 Ciphertext），进入人工审核。
- [[api_kyc_eid_retake_selfie]] `/kyc/active-account/v1/eid/main/retake-selfie` — liveness 失败后重新自拍，启动新的 signzy journey。
- [[api_kyc_eid_get_retake_selfie_result]] `/kyc/active-account/v1/eid/main/get-retake-selfie-result` — 获取重拍结果，分支与 get-result 类似，附带 retakeTooManyFlag。
- [[api_kyc_eid_leave_submit]] `/kyc/active-account/v1/eid/main/leave-submit` — 用户放弃 KYC 并记录 reason，不允许重新提交，前端无需校验响应。
- [[api_kyc_eid_verify_again]] `/kyc/active-account/v1/eid/main/verify-again` — 当 EID OCR 信息有误时重新发起 journey。

### Body Auth（活体核身）
- [[api_kyc_body_auth_apply]] `/kyc/body-auth/v1/liveness/apply` 与 `/kyc/body-auth/v2/liveness/apply` — 已认证用户活体核身入口；返回 model（HTTP / SDK）与 videoUrl；V2 的 videoUrl 由 config repo 中 `applyUrlV2` + signzy url 构成。
- [[api_kyc_body_unauth_apply]] `/kyc/body-unauth/v1/liveness/apply` — 未认证用户活体核身入口，需上送 mobile（Ciphertext）。
- 验证核身认证结果由各业务入口完成（参见 Eid kyc S-Model V1，已废弃）。

### 环境与 Partner URL
KYC / Liveness 在 CashNow、Botim、PayBy 三个 partner 下分别有 SIM/UAT 与 PROD 的 applyurl、redirecturl、contactUs 等配置，详见 [[kyc-partner-env-urls]]。

### 不在本次范围
- 重提交 EID（人工审核要求重新提交 EID）— 见 Eid kyc cgs api V1
- EID RENEW FLOW — 见 Eid kyc cgs api V1

各 channel 的端到端流程（含数据库变更、audit branch、channel 特有规则）见 [[kyc-channel-overview]] 中的 channel-specific 页面：UAEKYC — EID KYC Knowledge Base（含 Renew 流程）、UAE Pass — EID Verification via UAE Pass、Passport — Passport KYC via Signzy。

## QA 关注点
- 入门 QA 先读 Overview，再根据 case 打开对应 channel-specific 页面。
- 渠道判定依据：用户所持证件类型（EID vs Passport）+ 用户选择的验证方式（官方 UAE API / UAE Pass / Signzy）。
- KYC 是资金类操作（top-up、transfer、remittance）的前置条件；未完成则不能进行资金操作。
- 三个 channel（UAEKYC、UAE Pass、Passport）当前均 ACTIVE，须分别覆盖。
- inquire-info 返回的 kycStatus 中 PROCESS / BLOCKED / RESUBDOC / AUDIT 均不返回 KYC 信息；VIP 用户敏感字段以 `******` / `***************` 脱敏，需校验脱敏规则。
- start-journey / get-result / retake-selfie 等接口的响应使用 commandType（tips / moveForward / action）+ command
