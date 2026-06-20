---
id: api_kyc_passport_submit_ocr
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
- ocr
- signzy
- 临时方案
- 已暂停
subdomain: passport
module: null
sensitivity: normal
name: 提交护照OCR接口(signzy临时方案)
aliases: []
related_services: []
related_tables: []
related_scenarios:
- passport-kyc-flow
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
提交护照OCR识别信息，用于下线 mblink、使用 signzy 代替的临时方案。2025-10-10 新增，方案暂停。

## 路径/方法
- 路径：`/kyc/passport/v1/submit-ocr`
- 所属流程：护照KYC认证（[[passport-kyc-flow]]）

## 入参
业务请求：

| 名称 | 类型 | 非空 | 描述 |
|---|---|---|---|
| token | String | Y | 认证流程token |
| passportPageTag | String | Y | 护照页tag |

## 出参
业务响应（非200则不返回）：

| 名称 | 类型 | 非空 | 描述 | 样例 |
|---|---|---|---|---|
| nextStep | String | Y | 下一步骤：PP_OCR / PP_SUBMIT / PP_LIVENESS / AUDIT / DOWN | PP_SUBMIT |
| passportNo | String | Y | 护照编号密文 | |
| passportType | String | N | 护照类型 | |
| passportAvatarTag | String | Y | 护照头像 | |
| fullName | String | Y | 姓名密文 | |
| birthday | String | Y | 生日（yyyy-MM-dd） | |
| gender | String | Y | 性别 0:女，1:男 | |
| expiryDate | String | Y | 有效期（yyyy-MM-dd） | |
| issueDate | String | N | 签发日期（yyyy-MM-dd） | |
| issuePlace | String | N | 签发地 | |
| nationality | String | Y | 国籍code, 三位 | CHN |
| ocrServiceProvider | String | Y | ocr识别渠道 | signzy |

## 错误码
原文未列出明确错误码，仅约定"非200则不返回"业务响应字段。

## 测试校验点
- 该方案为临时替代 mblink 的过渡接口，状态为"暂停"，需确认是否启用。
- 入参仅 `token` 与 `passportPageTag`，OCR 字段由后端通过 signzy 识别返回，需校验返回的 `ocrServiceProvider=signzy`。
- nextStep 取值需在 {PP_OCR, PP_SUBMIT, PP_LIVENESS, AUDIT, DOWN} 范围内，正常分支为 `PP_SUBMIT`，后续衔接 [[api_kyc_passport_submit_v2]] (`/kyc/passport/v2/submit-passport`)。
- 校验密文字段（passportNo、fullName）的加密格式。
- 校验非空字段：token、passportPageTag、passportNo、passportAvatarTag、fullName、birthday、gender、expiryDate、nationality、ocrServiceProvider。
- 可空字段：passportType、issueDate、issuePlace。
