---
title: 护照KYC认证流程总览
domain: kyc
kind: wiki_page
slug: passport-kyc-flow
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki
source_ref: wiki:89009c95-2642-4856-b64c-da186d7ed287
tags: []
---

# 护照KYC认证流程总览

护照KYC认证通过文件上传、流程初始化、OCR识别、信息提交、活体认证等步骤串联完成，各步骤之间通过 `token` 关联，并以响应中的 `nextStep` 驱动下一步操作。

## 主流程步骤

按顺序执行的端到端流程：

1. **上传护照页、护照头像、活体视频包**：调用 `/upload` 接口（同KYC通用上传流程），获得对应的文件 tag。
2. **护照认证初始化**：调用 [[api_kyc_passport_init]]，传入 `bizType` 与 `bizData`，获取流程 `token` 与首个 `nextStep`。
3. **提交护照识别信息**：调用 [[api_kyc_passport_submit]]，提交护照页/头像 tag 及 OCR 解析得到的护照字段。
4. **活体认证**：调用 [[api_kyc_passport_liveness]]，提交 `livenessTag` 完成活体校验。

## nextStep 状态流转

各接口响应中的 `nextStep` 用于指示流程下一步，可能取值：

- `PP_OCR`：进入/重做护照 OCR 识别
- `PP_SUBMIT`：提交护照信息（v2 流程中使用）
- `PP_LIVENESS`：进入活体认证
- `AUDIT`：进入审核
- `DOWN`：流程终止/下线（响应中会带 `tips` 文案）

典型流转：

- v1 流程：`init → PP_OCR → submit-passport → PP_LIVENESS → liveness → AUDIT`
- v2 临时方案：`init → PP_OCR → submit-ocr → PP_SUBMIT → submit-passport(v2) → PP_LIVENESS → liveness → AUDIT`

当 `nextStep` 为 `AUDIT` 或 `DOWN` 时，接口会返回相应 `tips` 文案。

## v1 与 v2(signzy 临时方案) 的差异

为下线 mblink、使用 signzy 替代，新增了 v2 临时方案（2025-10-10 新增，方案暂停）：

- v1：客户端完成 OCR（如 `microblink`）后，直接调用 [[api_kyc_passport_submit]] 一次性提交护照页 tag 与解析字段。
- v2：拆为两步——先调用 [[api_kyc_passport_submit_ocr]] 仅提交 `passportPageTag`，由服务端通过 signzy 返回护照字段；再调用 [[api_kyc_passport_submit_v2]] 提交确认后的护照信息。
- v2 流程的 `ocrServiceProvider` 固定为 `signzy`；`nextStep` 集合中新增 `PP_SUBMIT`。

## 关键参数说明

- `token`：由初始化接口下发，贯穿后续所有步骤。
- `passportPageTag` / `passportAvatarTag` / `livenessTag`：均来自 `/upload` 接口返回的文件 tag。
- 加密字段：`passportNo`、`fullName` 以密文传输。
- 日期字段格式：`yyyy-MM-dd`（`birthday`、`expiryDate`、`issueDate`）。
- `gender`：`0` 女、`1` 男。
- `nationality`：三位国籍 code（如 `CHN`）。
- `ocrServiceProvider`：OCR 渠道（如 `microblink`、`signzy`）。

## 相关接口

- [[api_kyc_passport_init]] 护照认证初始化
- [[api_kyc_passport_submit]] 提交护照识别信息（v1）
- [[api_kyc_passport_liveness]] 护照活体认证
- [[api_kyc_passport_submit_ocr]] 提交护照OCR（signzy 临时方案）
- [[api_kyc_passport_submit_v2]] 提交护照信息（v2）
