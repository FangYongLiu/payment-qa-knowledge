---
id: api_kyc_passport_submit
object_type: API
domain: kyc
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-20'
source_type: wiki
source_ref: wiki:89009c95-2642-4856-b64c-da186d7ed287
tags:
- passport
- kyc
- microblink
subdomain: passport
module: submit
sensitivity: normal
name: 提交护照识别信息接口(v1)
aliases:
- /kyc/passport/v1/submit-passport
related_services: []
related_tables: []
related_scenarios:
- passport-kyc-flow
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
提交OCR识别后的护照信息（microblink方案），属于护照KYC流程中的提交识别信息环节，提交后由后端返回下一步骤（如活体认证、审核等）。

## 路径/方法
- 路径：`/kyc/passport/v1/submit-passport`
- 方法：业务请求（POST，遵循kyc通用约定）

## 入参
| 名称 | 类型 | 非空 | 描述 | 样例 |
|---|---|---|---|---|
| token | String | Y | 认证流程token | |
| passportPageTag | String | Y | 护照页tag | |
| passportAvatarTag | String | Y | 护照头像tag | |
| passportNo | String | Y | 护照编号密文 | |
| passportType | String | N | 护照类型 | |
| fullName | String | Y | 姓名密文 | |
| birthday | String | Y | 生日（yyyy-MM-dd） | |
| gender | String | Y | 性别 0:女，1:男 | |
| expiryDate | String | Y | 有效期（yyyy-MM-dd） | |
| issueDate | String | Y | 签发日期（yyyy-MM-dd） | |
| nationality | String | Y | 国籍code, 三位 | CHN |
| industry | String | Y | 行业 | Retail |
| ocrServiceProvider | String | Y | ocr识别渠道 | microblink |

## 出参
非200则不返回。

| 名称 | 类型 | 非空 | 描述 | 样例 |
|---|---|---|---|---|
| nextStep | String | Y | 下一步骤：PP_OCR / PP_LIVENESS / AUDIT / DOWN | PP_LIVENESS |
| tips | String | Y | 返回文案 | |

## 错误码
原文未列出具体错误码，仅约定"非200则不返回"业务响应。

## 测试校验点
- token 必须为有效的认证流程token，缺失或无效应被拒绝。
- 必填字段（passportPageTag、passportAvatarTag、passportNo、fullName、birthday、gender、expiryDate、issueDate、nationality、industry、ocrServiceProvider）缺失时应报错。
- passportType 可为空。
- birthday / expiryDate / issueDate 校验 yyyy-MM-dd 格式。
- gender 仅接受 0（女）/1（男）。
- nationality 必须为三位国籍code（如 CHN）。
- ocrServiceProvider 在本接口（v1）场景下为 microblink。
- passportNo、fullName 字段以密文传递。
- 响应 nextStep 取值范围限定：PP_OCR、PP_LIVENESS、AUDIT、DOWN；正常流程下应返回 PP_LIVENESS 进入活体认证（参见 [[api_kyc_passport_liveness]]）。
- 与 [[api_kyc_passport_init]] 衔接：init 返回 nextStep=PP_OCR 后进入本接口提交。
- 与 v2 方案区分：本接口为 microblink 渠道；signzy 临时方案见 [[api_kyc_passport_submit_ocr]] 与 [[api_kyc_passport_submit_v2]]。
