---
title: Passport KYC S-Model API 总览
domain: kyc
kind: wiki_page
slug: passport-kyc-s-model-api-overview
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki
source_ref: wiki:e75788c0-8dcd-4b0c-95e3-8c08067ad9e7
tags: []
related_services:
  - svc_kyc
related_tables:
  - tbl_kyc_tm_kyc_apply
  - tbl_kyc_tr_biz_record_passport
  - tbl_kyc_tr_biz_record_passport_live
  - tbl_kyc_tr_leave_record
---

# Passport KYC S-Model API 总览

本页汇总 Passport KYC 流程下的全部 S-Model API、统一的命令模型（commandType / commandData）以及端到端的调用顺序，便于快速定位每个接口在流程中的位置与作用。

## 环境域名

- SIM: `https://sim.test2pay.com/cgs/api`
- UAT: （待补充）
- PROD: （待补充）

所有请求与响应均为 JSON 协议。

## 接口清单

Passport KYC 主流程包含以下 6 个接口（均为 POST，路径前缀 `/kyc/active-account/v1/passport/main/`）：

| # | 接口 | 路径 | 作用 |
|---|------|------|------|
| 1 | [[api_kyc_passport_start_journey]] | `/start-journey` | 启动 journey，创建 journey URL；若用户已执行过则直接取结果 |
| 2 | [[api_kyc_passport_get_result]] | `/get-result` | 用户完成 journey 后，进入结果页并返回 KYC 结果 |
| 3 | [[api_kyc_passport_confirm_info]] | `/confirm-info` | 用户确认 Passport 信息（不可修改，不进入人工审核） |
| 4 | [[api_kyc_passport_retake_selfie]] | `/retake-selfie` | 活体校验失败后，用户选择重新拍摄自拍 |
| 5 | [[api_kyc_passport_verify_again]] | `/verify-again` | OCR 信息错误时，用户重新发起一次新的 journey |
| 6 | [[api_kyc_passport_leave_submit]] | `/leave-submit` | 用户放弃 KYC，记录放弃原因，且不允许再次提交 |

## 命令模型（commandType / commandData）

所有接口的响应统一使用 `commandType` + `commandData` 的命令模型驱动前端动作：

- `commandType = tips`：展示提示页/弹窗，`commandData` 为 `TipsInfo` 结构
- `commandType = moveForward`：进入下一步，`commandData` 为跳转 action
- `commandType = action`：携带业务数据（如 `passportInfo`）供前端继续处理

### TipsInfo 常用字段

- `type`：`Page` / `Popup`
- `title`、`tipText`、`tipContent`、`tipImg`
- `redirectView[]`：包含 `viewName`、`viewType`、`viewUrl`、`viewAction`

### moveForward 常用字段

- `nextStep`：下一步跳转地址，可为外链（如 signzy journey URL）或路由（如 `route://native/kyc/result`、`/kyc/home`）
- `data.token`：贯穿流程的 flow id

## 端到端调用顺序

典型 Passport KYC 流转：

1. 调用 [[api_kyc_passport_start_journey]]
   - 未做过 KYC：返回 `moveForward` + signzy journey URL，前端跳转开始 journey
   - 已做过：返回 `moveForward` 跳转结果页 `route://native/kyc/result`
2. 用户完成外部 journey 后，前端使用返回的 `token` 调用 [[api_kyc_passport_get_result]]，根据结果分支：
   - 活体失败 → `tips`，引导调用 [[api_kyc_passport_retake_selfie]]
   - KYC 处理中 / KYC 成功 / KYC 失败 → `tips` 展示对应文案
   - OCR 护照已过期 → `tips`，引导用户 Try again
   - 需要确认信息 → `action` 返回 `passportInfo`（`passportNumber`、`nameEnglish`、`birthDate`、`nationality`、`gender`、`expiryDate`，姓名与证件号需 RSA 加密）
3. 用户确认信息后调用 [[api_kyc_passport_confirm_info]]，根据响应进入失败/处理中/成功提示
4. 若 OCR 信息有误，用户可调用 [[api_kyc_passport_verify_again]] 重启一次新 journey（`nextStep=/kyc/home`）
5. 任意阶段用户放弃，调用 [[api_kyc_passport_leave_submit]] 上报 `reason`，且不允许再次提交，前端无需校验响应

## 通用约定

- 多数接口请求体仅包含 `token`（flow id），`start-journey` 例外，使用 `bizType` + `employeeId`
- 响应 `status=200` 表示成功
- 涉及证件信息的字段（姓名、证件号）需要 RSA 加密传输
- 日期字段格式统一为 `yyyy-MM-dd`
