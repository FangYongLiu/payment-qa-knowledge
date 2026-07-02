---
id: flow_kyc_passport
object_type: Flow
name: 护照 KYC 认证端到端流程 (Passport KYC)
aliases: [护照KYC流程, passport-kyc-flow, passport-auth-flow, Passport S-Model]
domain: activation
status: active
owner: xinwei.cao
reviewer: xinwei.cao
last_reviewed_at: '2026-06-25'
source_type: wiki
source_ref: legacy/wiki/kyc/passport-kyc-flow.md + kyc-passport-auth-flow.md + passport-kyc-s-model-api-overview.md(整合)
tags: [kyc, passport, 护照, signzy, 流程]
related_services: [svc_kyc, svc_outman]
related_tables: [tbl_kyc_tr_biz_record_passport, tbl_kyc_tr_biz_record_passport_live, tbl_kyc_tm_kyc_apply]
related_scenarios: []
---

# 护照 KYC 认证端到端流程 (Passport KYC)

> 面向无 EID 的 WPS workers,底层 provider 为 Signzy。以流程 `token` 为主线,各步骤由响应 `nextStep` 驱动状态流转。

## 概述
护照 KYC 依次经历:**上传与初始化 → OCR 识别 → 护照信息保存 → 活体检测 → 活体校验与人脸比对 → 审核提交**。
参与方:Botim App(客户端)、CGS(上传/初始化网关)、[[svc_kyc]](KYC 业务)、[[svc_outman]](对接 Signzy 的外呼/文件服务)、Signzy(第三方 KYC 能力)。

## 步骤(跨系统)
1. **上传文件**:Botim App → CGS `/upload` 上传护照页/头像/活体视频包,得到 tag。
2. **初始化**:[[api_kyc_passport_init]](`/kyc/passport/v1/init`),传 `bizType`/`bizData`,返回流程 `token` 与首个 `nextStep`。
3. **OCR 识别**:[[api_kyc_passport_submit_ocr]] → kyc → outman → Signzy 执行 OCR → 回传护照信息。
4. **护照信息保存**:[[api_kyc_passport_submit_passport_v1]](确认后 `save passport info` 落库 → [[tbl_kyc_tr_biz_record_passport]])。
5. **活体检测**:Botim App 本地依图(yitu)SDK 采集。
6. **活体校验 + 人脸比对**:[[api_kyc_passport_liveness]] → kyc → outman(取活体照)→ Signzy `face match`(与护照照比对)→ 返回结果(落 [[tbl_kyc_tr_biz_record_passport_live]])。
7. **审核 / 结束**:`nextStep` 流转至 `AUDIT`(人审)或 `DOWN`(结束),由 `tips` 返回文案。

## nextStep 状态枚举
`PP_OCR`(护照 OCR 提交)、`PP_SUBMIT`(护照信息提交,v2 用)、`PP_LIVENESS`(活体)、`AUDIT`(人审)、`DOWN`(结束/下线,配 tips 文案)。
- **标准路径**:`init → PP_OCR → submit-passport(v1) → PP_LIVENESS → liveness → AUDIT`(`ocrServiceProvider=microblink`)。
- **Signzy 临时方案(2025-10 新增,已暂停)**:`init → PP_OCR → submit-ocr → PP_SUBMIT → submit-passport(v2) → PP_LIVENESS → liveness → AUDIT`(provider=signzy);见 [[api_kyc_passport_submit_ocr]]、[[api_kyc_passport_submit_passport_v2]]。
- 任意步骤命中风控/终态 → `nextStep` 直接 `AUDIT`/`DOWN` + tips。

## 关联关系
- **经过的服务**:[[svc_kyc]] → [[svc_outman]] → Signzy(外部)
- **读写的表**:[[tbl_kyc_tr_biz_record_passport]]、[[tbl_kyc_tr_biz_record_passport_live]]、[[tbl_kyc_tm_kyc_apply]]
- **相关接口**:[[api_kyc_passport_init]]、[[api_kyc_passport_submit_passport_v1]]、[[api_kyc_passport_liveness]]、[[api_kyc_passport_get_result]] 等(见 service_gp078_kyc)

## 校验点
- 流程 `token` 由 init 下发,后续所有步骤接口必须透传;`token` 与各 `tr_biz_record_*.req_token` 一致。
- `nextStep` 状态机流转正确;非 200 时不返回业务响应体。
- `passportNo`/`fullName` 等敏感字段密文传输。
- `ocrServiceProvider` 区分通道(microblink v1 / signzy 临时);signzy 路径已暂停,回归勿走。
- 活体不清晰 → 重拍([[api_kyc_passport_retake_selfie]]);人脸比对分数阈值。
