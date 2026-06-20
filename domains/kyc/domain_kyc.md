---
id: domain_kyc
object_type: Domain
domain: kyc
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-20'
source_type: wiki
source_ref: confluence:PMDPayment/1089405294
tags:
- KYC
- EID
- 身份验证
- 活体认证
subdomain: null
module: null
sensitivity: normal
name: KYC身份验证业务域
aliases: []
related_services: []
related_tables: []
related_scenarios:
- eid-kyc-cgs-api-overview
- eid-kyc-environment-urls
related_logs: []
related_requirements: []
related_failures: []
---

## 概述
KYC (Know Your Customer) 是 Botim App 用户在进行任何资金相关交易（top-up、transfer、remittance 等）之前必须完成的身份验证业务域。用户进入 Botim App 后，需要先通过 KYC 才能开通资金类功能。KYC 可通过多个渠道（channel）完成，具体走哪个渠道取决于用户持有的证件类型以及其选择的验证方式。

本业务域同时承载 EID KYC CGS API V2 接口集，定义了从 KYC 状态提醒、EID 旅程启动、OCR/活体校验、信息确认/编辑、放弃 KYC 到活体认证 (Body Auth) 的完整后端协议。所有请求与响应使用 JSON。

## 覆盖范围
本业务域覆盖以下三个 ACTIVE 渠道：

- **UAEKYC**：基于 Emirates ID (EID)，底层走官方 UAE API，是大多数用户使用的主渠道（primary channel）。
- **UAE Pass**：基于 EID，通过 UAE Pass App 完成；底层 provider 为 UAE Pass（政府数字身份）；面向偏好使用 UAE Pass 验证的用户。
- **Passport**：基于护照（Passport），底层 provider 为 Signzy；面向没有 EID 的 WPS workers。

CGS API V2 接口集涵盖：
- EID KYC 主流程：check-reminder、inquire-info、start-journey、get-result、inquire-industry、confirm-info、submit-edit、retake-selfie、get-retake-selfie-result、leave-submit、verify-again
- Body Auth 活体认证：authed apply (v1/v2)、unauthed apply (v1)
- 多业务方 (CashNow / Botim / PayBy) SIM/UAT/PROD URL 配置

## 关键服务/流程
每个渠道都有独立的 end-to-end 流程文档，包含各步骤的数据库变更、审计分支（audit branch）以及该渠道特有的规则：

- UAEKYC — EID KYC Knowledge Base（含 Renew 流程）
- UAE Pass — EID Verification via UAE Pass
- Passport — Passport KYC via Signzy

CGS API V2 主要接口：
- [[api_kyc_check_reminder]] `/kyc/active-account/v1/kyc/check-reminder`：检查 KYC 状态并提醒用户尽快确认 EID 信息
- [[api_kyc_inquire_info]] `/kyc/active-account/v1/kyc/inquire-info`：查询用户 KYC 信息，返回 kycStatus（NON/PROCESS/FINISH/EXPIRED/BLOCKED/RESUBDOC/AUDIT）、eidInfo、passportInfo
- [[api_kyc_eid_start_journey]] `/kyc/active-account/v1/eid/main/start-journey`：启动 EID 旅程，返回 commandType（tips/moveForward）和 nextStep（HTTP/TOKEN 模式 signzy URL，或 native 路由 result/re-submit 页）
- [[api_kyc_eid_get_result]] `/kyc/active-account/v1/eid/main/get-result`：拉取旅程结果，分支包含 liveness fail、kyc process(48h 审核)、confirm（含 manualEditFlag、eidInfo）、re-submit、kyc success、kyc fail、ocr eid expired
- [[api_kyc_eid_inquire_industry]] `/kyc/active-account/v1/eid/inquire-industry`：返回 industryList（value/name）
- [[api_kyc_eid_confirm_info]] `/kyc/active-account/v1/eid/main/confirm-info`：用户不修改时确认 EID，无需人工审核；可走 kyc fail/process/success 或切换 mobile (choose-account)
- [[api_kyc_eid_submit_edit]] `/kyc/active-account/v1/eid/main/submit-edit`：用户修改后提交，进入人工审核；idNumber/name 需 RSA 密文
- [[api_kyc_eid_retake_selfie]] `/kyc/active-account/v1/eid/main/retake-selfie`：活体失败时重新自拍，返回 signzy nextStep
- [[api_kyc_eid_get_retake_selfie_result]] `/kyc/active-account/v1/eid/main/get-retake-selfie-result`：拉取重拍结果，含 retakeTooManyFlag 标志
- [[api_kyc_eid_leave_submit]] `/kyc/active-account/v1/eid/main/leave-submit`：放弃 KYC，记录 reason，前端无需校验响应，不允许重新提交
- [[api_kyc_eid_verify_again]] `/kyc/active-account/v1/eid/main/verify-again`：OCR 信息错误时发起新的旅程，nextStep 跳 `/kyc/home`
- [[api_kyc_body_auth_apply]] `/kyc/body-auth/v1/liveness/apply` 与 `/kyc/body-auth/v2/liveness/apply`：已认证用户活体；V2 的 videoUrl 走 config repo `applyUrlV2` + signzy url
- [[api_kyc_body_unauth_apply]] `/kyc/body-unauth/v1/liveness/apply`：未认证用户活体（含 mobile 密文参数）

详见 [[eid-kyc-cgs-api-overview]] 与 [[eid-kyc-environment-urls]]。

## QA 关注点
- 入门 QA 应先阅读本 Overview，再根据具体 case 打开对应的 channel-specific 页面。
- 区分用户走哪个 channel 的判定依据：所持证件类型（EID vs Passport）以及用户选择的验证方式（官方 UAE API、UAE Pass、Signzy）。
- KYC 是资金类操作的前置条件，验证未完成则不能进行 top-up/transfer/remittance。三个 channel 当前状态均为 ACTIVE，QA 需分别覆盖。
- 关注 kycStatus 取值：FINISH/PROCESS/AUDIT/BLOCKED/RESUBDOC 时是否返回 eidInfo（PROCESS/BLOCKED/RESUBDOC/AUDIT 不返回）；VIP 用户敏感字段是否脱敏为 `*`。
- 校验 commandType 协议：`tips` (展示提示页/弹窗) 与 `moveForward` (跳转 nextStep)；nextStep 包含 HTTP signzy URL、TOKEN 模式 token、`route://native/kyc/result`、`route://native/kyc/re-submit`、`/kyc/home`、`/kyc/choose-account` 等多种形态。
- submit-edit 与 confirm-info 的差异：是否触发人工审
