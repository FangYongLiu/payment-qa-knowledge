---
id: api_kyc_passport_liveness
object_type: API
domain: kyc
status: active
owner: xinwei.cao
reviewer: xinwei.cao
last_reviewed_at: '2026-06-20'
source_type: wiki
source_ref: confluence:PMDPayment/205914971
tags: []
subdomain: passport
module: null
sensitivity: normal
name: 护照活体认证接口
aliases: []
related_services:
- svc_kyc
---

## 用途
活体验证：在护照KYC流程中提交活体视频包，完成活体认证。

## 路径/方法
- 路径：/kyc/passport/v1/liveness

## 入参
业务请求：

| 名称 | 类型 | 非空 | 描述 |
|---|---|---|---|
| token | String | Y | 认证流程token |
| livenessTag | String | Y | 活体视频包 |

## 出参
业务响应（非200则不返回）：

| 名称 | 类型 | 非空 | 描述 | 样例 |
|---|---|---|---|---|
| nextStep | String | Y | 下一步骤：PP_OCR / PP_LIVENESS / AUDIT / DOWN | AUDIT |
| tips | String | Y | 返回文案 | - |

## 错误码
原文未列出错误码；约定非200则不返回业务响应。

## 测试校验点
- token 必传，需为有效的认证流程 token（来自 init 或上一步骤）。
- livenessTag 必传，对应 /upload 上传得到的活体视频包 tag。
- 校验 nextStep 取值范围：PP_OCR、PP_LIVENESS、AUDIT、DOWN；正常通过后应推进至 AUDIT。
- 非200状态下不应返回业务响应字段。
- 校验 tips 文案在不同 nextStep（如 AUDIT/DOWN）下是否正确返回。
