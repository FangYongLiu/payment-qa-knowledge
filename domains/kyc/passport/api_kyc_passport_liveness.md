---
id: api_kyc_passport_liveness
object_type: API
domain: kyc
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-20'
source_type: wiki
source_ref: wiki:89009c95-2642-4856-b64c-da186d7ed287
tags:
- 护照
- 活体
- KYC
subdomain: passport
module: null
sensitivity: normal
name: 护照活体认证接口
aliases:
- /kyc/passport/v1/liveness
related_services: []
related_tables: []
related_scenarios:
- passport-kyc-flow
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
活体验证：在护照KYC流程中提交活体视频包，完成活体认证步骤。

## 路径/方法
- 路径：/kyc/passport/v1/liveness

## 入参
业务请求：

| 名称 | 类型 | 非空 | 描述 | 样例 |
|---|---|---|---|---|
| token | String | Y | 认证流程token | |
| livenessTag | String | Y | 活体视频包 | |

## 出参
业务响应（非200则不返回）：

| 名称 | 类型 | 非空 | 描述 | 样例 |
|---|---|---|---|---|
| nextStep | String | Y | 下一步骤：PP_OCR / PP_LIVENESS / AUDIT / DOWN | AUDIT |
| tips | String | Y | 返回文案 | |

## 错误码
原文未列出具体错误码，仅说明"非200则不返回"业务响应。

## 测试校验点
- token 必传，且为有效的认证流程 token。
- livenessTag 必传，对应已通过 /upload 上传的活体视频包。
- 校验响应 nextStep 取值在 {PP_OCR, PP_LIVENESS, AUDIT, DOWN} 范围内；活体通过后通常应进入 AUDIT。
- 当 nextStep 为 AUDIT 或 DOWN 时，校验 tips 文案返回。
- 非200状态时校验不返回业务响应体。
