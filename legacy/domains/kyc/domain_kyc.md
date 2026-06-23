---
id: domain_kyc
object_type: Domain
domain: kyc
status: archived
owner: wiki-sync@acquire
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-20'
source_type: wiki
source_ref: confluence:PMDPayment/1446215797
tags:
- kyc
- passport
- s-model
subdomain: null
module: null
sensitivity: normal
name: KYC身份验证业务域
aliases: []
related_services:
- api_kyc_passport_start_journey
- api_kyc_passport_get_result
- api_kyc_passport_confirm_info
- api_kyc_passport_retake_selfie
- api_kyc_passport_verify_again
- api_kyc_passport_leave_submit
related_tables: []
related_scenarios:
- passport-kyc-s-model-api-overview
related_logs: []
related_requirements: []
related_failures: []
---

## 概述
KYC (Know Your Customer) 是 Botim App 用户在进行任何资金相关交易（top-up、transfer、remittance 等）之前必须完成的身份验证业务域。用户进入 Botim App 后，需要先通过 KYC 才能开通资金类功能。KYC 可通过多个渠道（channel）完成，具体走哪个渠道取决于用户持有的证件类型以及其选择的验证方式。

## 覆盖范围
本业务域覆盖以下三个 ACTIVE 渠道：

- **UAEKYC**：基于 Emirates ID (EID)，底层走官方 UAE API，是大多数用户使用的主渠道（primary channel）。
- **UAE Pass**：基于 EID，通过 UAE Pass App 完成；底层 provider 为 UAE Pass（政府数字身份）；面向偏好使用 UAE Pass 验证的用户。
- **Passport**：基于护照（Passport），底层 provider 为 Signzy；面向没有 EID 的 WPS workers。Passport 渠道下还包含 S-Model 子流程，提供一组独立的 API 用于驱动 journey、获取结果、确认信息、重拍 selfie、重新验证以及放弃 KYC。

## 关键服务/流程
每个渠道都有独立的 end-to-end 流程文档，包含各步骤的数据库变更、审计分支（audit branch）以及该渠道特有的规则：

- UAEKYC — EID KYC Knowledge Base（含 Renew 流程）
- UAE Pass — EID Verification via UAE Pass
- Passport — Passport KYC via Signzy
  - Passport KYC S-Model API 流程（参见 [[passport-kyc-s-model-api-overview]]），包含：
    - [[api_kyc_passport_start_journey]] `/kyc/active-account/v1/passport/main/start-journey`：启动 journey，创建 journey url；若用户已完成则直接返回结果。
    - [[api_kyc_passport_get_result]] `/kyc/active-account/v1/passport/main/get-result`：用户完成 journey 后获取 KYC 结果（含 liveness fail / kyc process / confirm / kyc success / kyc fail / passport expired 等分支）。
    - [[api_kyc_passport_confirm_info]] `/kyc/active-account/v1/passport/main/confirm-info`：用户确认 OCR 出来的护照信息，不可修改，且不进入人工审核。
    - [[api_kyc_passport_retake_selfie]] `/kyc/active-account/v1/passport/main/retake-selfie`：liveness 失败时重新拍 selfie，触发新的 signzy journey。
    - [[api_kyc_passport_verify_again]] `/kyc/active-account/v1/passport/main/verify-again`：OCR 出的护照信息错误时重新发起新的 journey。
    - [[api_kyc_passport_leave_submit]] `/kyc/active-account/v1/passport/main/leave-submit`：用户放弃 KYC，记录放弃原因，不允许再次提交，前端无需校验响应。

详见 [[kyc-channel-overview]]。

## QA 关注点
- 入门 QA 应先阅读本 Overview，再根据具体 case 打开对应的 channel-specific 页面。
- 区分用户走哪个 channel 的判定依据：所持证件类型（EID vs Passport）以及用户选择的验证方式（官方 UAE API、UAE Pass、Signzy）。
- 注意 KYC 是资金类操作的前置条件，验证未完成则不能进行 top-up/transfer/remittance。
- 三个 channel 当前状态均为 ACTIVE，QA 需分别覆盖。
- Passport S-Model 流程要点：
  - 所有请求/响应均为 JSON；响应中通过 `commandType` 区分 `tips`（展示提示）/ `moveForward`（进入下一步）/ `action`（确认信息），需覆盖各分支。
  - `passportInfo` 中的 `nameEnglish` 与 `passportNumber` 需 RSA 加密；字段还包括 `birthDate`(yyyy-MM-dd)、`nationality`、`gender`、`expiryDate`(yyyy-MM-dd)。
  - `token` 作为 flow id 在 start-journey 之后的所有 API 中传递，需校验其与 journey 状态一致性。
  - get-result 中 `redirectView` 的 `viewAction.retakeTooManyFlag=Y` 表示重拍次数过多，需阻断重试。
  - leave-submit 提交后不可恢复 KYC，需验证后续接口的拦截逻辑。
  - 关注 OCR 护照过期分支（"Your Passport has expired"），用户需提供新护照重新走 journey。
