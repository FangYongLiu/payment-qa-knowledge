---
title: 护照KYC认证流程
domain: kyc
kind: wiki_page
slug: passport-kyc-flow
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:b2a9f353-22d0-401c-a0b5-b9fcd72d4ea8
tags: []
---

# 护照KYC认证流程

本页描述员工发起护照KYC后，从证件上传、OCR识别、活体检测到人脸比对与审核提交的端到端系统交互流程（参见 [[domain_kyc]]）。

## 参与方

- Emplyee：发起KYC的员工
- Botim App：客户端
- Cgs：护照上传与初始化网关
- Kyc：KYC业务服务
- Outman：KYC外呼/对接服务
- Signzy：第三方KYC能力提供方

## 总体阶段

护照KYC流程依次经历：上传与初始化 → OCR识别 → 护照信息保存 → 活体检测 → 活体校验与人脸比对 → 审核提交。

## 上传与初始化

1. Emplyee 在 Botim App 发起 `start passport kyc`。
2. Botim App → Cgs：`upload passport`，上传护照图片。
3. Botim App → Cgs：`/kyc/passport/v1/init`，初始化护照KYC会话。

## OCR 识别

1. Botim App → Kyc：`/kyc/passport/v1/submit-ocr`。
2. Kyc → Outman：`passport ocr`。
3. Outman → Signzy：`submit ocr`，由 Signzy 执行OCR。
4. Kyc → Botim App：`return passport info`，回传识别出的护照信息。

## 护照信息保存

1. Botim App → Kyc：`/kyc/passport/v2/submit-passport`，提交确认后的护照信息。
2. Kyc 内部自调用 `save passport info`，落库保存。

## 活体检测

1. Botim App 本地自调用 `liveness(yitu sdk)`，使用依图（yitu）SDK 完成活体采集。

## 活体校验与人脸比对

1. Botim App → Kyc：`/kyc/passport/v1/liveness`。
2. Kyc → Outman：`liveness verify`。
3. Outman 自调用 `get liveness photos`，获取活体照片。
4. Outman → Signzy：`face match`，与护照照片进行人脸比对。
5. Outman → Kyc：返回比对结果。

## 审核提交与返回

1. Kyc → Outman：`submit audit`，提交审核。
2. Kyc → Botim App：返回活体接口结果。
3. Botim App 向上返回最终结果给 Emplyee。

## 关键接口一览

| 步骤 | 接口 / 动作 | 调用方向 |
|---|---|---|
| 上传 | `upload passport` | Botim App → Cgs |
| 初始化 | `/kyc/passport/v1/init` | Botim App → Cgs |
| 提交OCR | `/kyc/passport/v1/submit-ocr` | Botim App → Kyc |
| 提交护照 | `/kyc/passport/v2/submit-passport` | Botim App → Kyc |
| 活体采集 | `liveness(yitu sdk)` | Botim App 本地 |
| 活体校验 | `/kyc/passport/v1/liveness` | Botim App → Kyc |
| 人脸比对 | `face match` | Outman → Signzy |
| 审核提交 | `submit audit` | Kyc → Outman |
