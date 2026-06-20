---
title: Passport KYC S-Model API 总览
domain: kyc
kind: wiki_page
slug: passport-kyc-s-model-api-overview
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:PMDPayment/1446215797
tags: []
---

# Passport KYC S-Model API 总览

本页汇总护照（Passport）KYC 主流程的 S-Model 接口集合，涵盖启动旅程、获取结果、确认信息、重拍自拍、重新验证以及放弃 KYC，并说明通用响应结构 `commandType` / `commandData` 的语义。所属业务域见 [[domain_kyc]]。

## 接入域名

- SIM: `https://sim.test2pay.com/cgs/api`
- UAT / PROD: 同结构（域名按环境替换）
- 协议：所有请求/响应 body 均为 JSON

## 接口清单

护照 KYC 主流程接口（路径前缀 `/kyc/active-account/v1/passport/main/`）：

| 功能 | 路径 | 说明 |
|---|---|---|
| 启动护照 KYC 旅程 | `/start-journey` | 创建 journey URL；若已执行过则返回结果。详见 [[api_kyc_passport_start_journey]] |
| 获取 KYC 结果 | `/get-result` | 用户完成旅程后跳转结果页并返回结果。详见 [[api_kyc_passport_get_result]] |
| 确认护照信息 | `/confirm-info` | 用户确认 OCR 信息，不可修改，且不进入人工审核。详见 [[api_kyc_passport_confirm_info]] |
| 重新自拍 | `/retake-selfie` | 活体认证失败时，用户选择再次自拍。详见 [[api_kyc_passport_retake_selfie]] |
| 重新验证 | `/verify-again` | 当 OCR 护照信息有误时，用户重新发起新的 journey。详见 [[api_kyc_passport_verify_again]] |
| 放弃 KYC | `/leave-submit` | 记录用户放弃 KYC 的原因；不允许再次提交，前端无需校验响应。详见 [[api_kyc_passport_leave_submit]] |

所有接口 Method 均为 `POST`，`status=200` 表示成功。

## 通用响应结构

业务响应统一通过 `commandType` + `commandData` 两字段驱动前端跳转或提示：

### commandType 取值

- `tips`：展示提示页/弹窗（`commandData` 为 TipsInfo）
- `moveForward`：进入下一步（`commandData` 包含 `nextStep` 等动作信息）
- `action`：返回业务数据动作（如 `get-result` 中返回 `passportInfo` 供用户确认）

### commandData 形态

- 当 `commandType = tips`：返回 TipsInfo，常见字段包括 `type`（`Page` / `Popup`）、`title`、`tipText`、`tipContent`、`tipImg`，以及 `redirectView` 数组（含 `viewName`、`viewType`、`viewUrl`、`viewAction`）。
- 当 `commandType = moveForward`：返回下一步信息，如 `nextStep`（外部 URL，例如 `https://kyc-preproduction.signzy.app/...`，或路由如 `route://native/kyc/result`、`/kyc/home`）以及 `data.token`。
- 当 `commandType = action`：返回结构化业务字段（如 `passportInfo`）。

## passportInfo 结构

`get-result` 在 `commandType = action` 时返回的护照信息（姓名与护照号需 RSA 加密）：

| 字段 | 类型 | 必填 | 示例 | 说明 |
|---|---|---|---|---|
| passportNumber | String | Y | 784XXXXXXXXXX | 护照号（Eid 上的号码） |
| nameEnglish | String | Y | SanZhang | 英文名 |
| birthDate | String | Y | 1992-01-01 | yyyy-MM-dd |
| nationality | String | Y | India | 国籍 |
| gender | String | Y | Male | 性别 |
| expiryDate | String | Y | 2026-12-01 | yyyy-MM-dd |

## 通用流转语义

- `token`：贯穿 `get-result`、`confirm-info`、`retake-selfie`、`verify-again`、`leave-submit` 的 flow id，由 `start-journey` 在 `commandData.data.token` 中下发。
- 典型 tips 场景：`Kyc fail`（失败可重试/不可重试）、`We are verifying your account`（人工审核中，最长 48 小时）、`Kyc success`（账户已激活）、`Your Passport has expired`（OCR 检测到护照过期，提示提供新护照）。
- 失败可触发的后续动作通过 `redirectView` 暴露，例如 `Retake selfie`（携带 `retakeTooManyFlag`）、`Try again`、`Okay` 等。
