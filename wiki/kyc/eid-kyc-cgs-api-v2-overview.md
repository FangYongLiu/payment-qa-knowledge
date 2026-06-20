---
title: EID KYC CGS API V2 总览
domain: kyc
kind: wiki_page
slug: eid-kyc-cgs-api-v2-overview
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki
source_ref: wiki:c77c6bdf-23d4-4c31-b325-128a8f8a6d3e
tags: []
---

# EID KYC CGS API V2 总览

EID KYC CGS API V2 提供 EID 实名认证、活体核身（Body Auth）以及相关查询/确认/重做能力，所有接口走 JSON 协议，挂载在 `cgs/api` 域下。本页给出接口分组、整体编排和与 V1 的差异说明，详细字段见各接口子页。

## 接口分组

### EID KYC FLOW（`/kyc/active-account/v1/...`）
- [[api_kyc_check_reminder]] `kyc/check-reminder` — 检查 KYC 状态并提示用户尽快确认 EID 信息
- [[api_kyc_inquire_info]] `kyc/inquire-info` — 查询用户 KYC 信息（含 `kycStatus`、`eidInfo`、`passportInfo`）
- [[api_kyc_eid_start_journey]] `eid/main/start-journey` — 启动 KYC Journey，创建 Journey URL；已执行过则返回结果
- [[api_kyc_eid_get_result]] `eid/main/get-result` — 获取 Journey 结果，引导至 confirm/重提交/成功/失败
- [[api_kyc_eid_inquire_industry]] `eid/inquire-industry` — 查询行业列表供用户选择
- [[api_kyc_eid_confirm_info]] `eid/main/confirm-info` — 用户确认 EID 信息（不修改，不进入人工审核）
- [[api_kyc_eid_submit_edit]] `eid/main/submit-edit` — 用户修改后提交 EID 信息（进入人工审核）
- [[api_kyc_eid_retake_selfie]] `eid/main/retake-selfie` — 活体失败时重新自拍，启动新 Journey
- [[api_kyc_eid_get_retake_selfie_result]] `eid/main/get-retake-selfie-result` — 获取重拍 Journey 结果
- [[api_kyc_eid_leave_submit]] `eid/main/leave-submit` — 用户放弃 KYC，记录原因，不允许重提交
- [[api_kyc_eid_verify_again]] `eid/main/verify-again` — OCR 信息错误时发起新 Journey

### Body Auth（活体核身）
- [[api_kyc_body_auth_apply]] `/kyc/body-auth/v1/liveness/apply` 与 `/kyc/body-auth/v2/liveness/apply` — 已认证用户活体核身申请
- [[api_kyc_body_unauth_apply]] `/kyc/body-unauth/v1/liveness/apply` — 未认证用户活体核身申请（请求需带加密 `mobile`）

## 调用流程编排

主流程（首次 KYC）：
1. `check-reminder` / `inquire-info` 判定当前 `kycStatus`（`NON / PROCESS / FINISH / EXPIRED / BLOCKED / RESUBDOC / AUDIT`）
2. `start-journey` 拿到 `nextStep`（HTTP 跳 signzy URL，或 TOKEN 模式给 native）
3. Journey 完成后 `get-result`：
   - `commandType=tips` → 展示页面/弹窗（成功 / 失败 / 处理中 / EID 已过期等）
   - `commandType=action` → 进入 confirm 页，回显 `eidInfo`（`name`、`idNumber` 为 RSA 密文）
   - `commandType=moveForward` 且 `nextStep=route://native/kyc/re-submit` → 进入重提交页
4. confirm 页两条分支：
   - 不修改 → `confirm-info`（不进人工审核）
   - 有修改 → `submit-edit`（进人工审核），需传密文 `idNumber`、`name`，以及 `birthDate`、`expiryDate`、`industry`
5. `industry` 取值由 `inquire-industry` 返回的 `industryList[].value` 提交

异常分支：
- 活体失败 → `retake-selfie` 重新发起 → `get-retake-selfie-result`，`retakeTooManyFlag=Y` 表示已超次数
- OCR 字段不正确 → `verify-again` 重新走整个 Journey（`nextStep=/kyc/home`）
- 主动放弃 → `leave-submit` 提交 `reason`

响应统一约定：
- `commandType`：`tips`（展示 TipsInfo） / `moveForward`（跳转下一步） / `action`（进入业务确认）
- `commandData` 内 `type` 为 `Page` 或 `Popup`，可带 `redirectView` 列出多个跳转按钮（如 `Retake selfie`、`Verify with UAE PASS`、`Try again`、`Contact us`）

## V1 / V2 差异

- 主体 EID KYC 接口仍挂在 `v1` 路径（`/kyc/active-account/v1/...`）；本页归类为 V2 总览，是相对于已废弃的 "Eid kyc S-Model V1" 流程整理的最新接口集。
- Body Auth 新增 V2：`/kyc/body-auth/v2/liveness/apply`
  - 与 V1 入参/出参字段相同（`ticket`、`redirectUrl` / `model`、`videoUrl`）
  - V2 的 `videoUrl` 由配置仓 `applyUrlV2` 指定的 Web 地址 + signzy URL 拼接（示例：`https://uat-identity.test2pay.com/biometric?pbw_show_title=N&partner=botim&url=...`）
  - V1 走的是「小程序地址 + signzy URL」并需后端 encodeUrl
- 不在本次范围：重提交 EID（人工审核要求重新提交）和 EID RENEW FLOW，仍参见 V1 文档

## 数据与加密说明

- `get-result` 与 `get-retake-selfie-result` 返回的 `eidInfo` 中 `name`、`idNumber` 需要 RSA 加密
- `submit-edit` 的 `idNumber`、`name` 上送时也为密文
- `inquire-info` 对 VIP 用户的 `cardNo`、`idNumber`、`nameEnglish`、`passportInfo` 等字段会以 `***` 脱敏返回
- `kycStatus` 中 `PROCESS / BLOCKED / RESUBDOC / AUDIT` 状态不返回 KYC 详细信息

## 环境与各业务方 URL

各业务方（CashNow / Botim / PayBy）在 SIM/UAT/PROD 下的 KYC `applyurl`、活体 `liveness-applyurl`、`redirecturl`、`contactUs` 等地址，详见 [[kyc-partner-env-urls]]。

业务域整体定位与上下游关系参见 [[domain_kyc]]。
