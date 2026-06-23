---
title: 护照KYC认证流程总览
domain: kyc
kind: wiki_page
slug: kyc-passport-auth-flow
status: archived
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:PMDPayment/205914971
tags: []
---

# 护照KYC认证流程总览

护照KYC认证以流程token为主线，按上传文件 → 初始化 → OCR/护照信息提交 → 活体认证 → 审核的顺序推进，各步骤通过响应中的 `nextStep` 字段驱动状态流转。

## 流程步骤

1. **上传文件**：通过 `/upload` 接口上传护照页、护照头像、活体视频包，得到对应的 tag（同通用KYC上传逻辑）。
2. **护照认证初始化**：调用 [[api_kyc_passport_init]]，传入 `bizType` 与 `bizData`，返回流程 `token` 与首个 `nextStep`。
3. **提交护照识别信息**：根据 `nextStep`，调用 [[api_kyc_passport_submit_passport_v1]] 上送护照页/头像 tag 与 OCR 识别字段。
4. **活体认证**：调用 [[api_kyc_passport_liveness]]，提交 `livenessTag` 完成活体校验。
5. **审核 / 结束**：`nextStep` 流转至 `AUDIT` 或 `DOWN` 时，由 `tips` 返回相应文案。

## nextStep 状态枚举

各业务接口响应中可能返回的下一步标识：

- `PP_OCR`：进入护照 OCR 识别提交环节
- `PP_SUBMIT`：进入护照信息提交环节（v2 流程使用）
- `PP_LIVENESS`：进入活体认证环节
- `AUDIT`：进入审核
- `DOWN`：流程结束/下线，配合 `tips` 提示文案

## 典型流转路径

- 标准路径：`init` → `PP_OCR` → submit-passport(v1) → `PP_LIVENESS` → liveness → `AUDIT`
- signzy 临时方案路径（2025-10-10 新增，**方案暂停**）：`init` → `PP_OCR` → submit-ocr → `PP_SUBMIT` → submit-passport(v2) → `PP_LIVENESS` → liveness → `AUDIT`
- 任意步骤命中风控或终态时，`nextStep` 直接返回 `AUDIT` 或 `DOWN`，并附带 `tips` 文案。

## 关键约束

- 所有业务接口在非200时不返回业务响应体。
- 流程 `token` 由 init 接口下发，后续所有步骤接口均需透传。
- `passportNo`、`fullName` 等敏感字段以密文形式传输。
- `ocrServiceProvider` 标识 OCR 渠道：v1 流程示例为 `microblink`，临时方案为 `signzy`。

## 接口索引

- [[api_kyc_passport_init]] —— 流程初始化 `/kyc/passport/v1/init`
- [[api_kyc_passport_submit_passport_v1]] —— 提交护照识别信息 `/kyc/passport/v1/submit-passport`
- [[api_kyc_passport_liveness]] —— 活体认证 `/kyc/passport/v1/liveness`
- [[api_kyc_passport_submit_ocr]] —— 提交护照OCR（signzy 临时方案，已暂停）`/kyc/passport/v1/submit-ocr`
- [[api_kyc_passport_submit_passport_v2]] —— 提交护照信息 v2（signzy 临时方案，已暂停）`/kyc/passport/v2/submit-passport`
