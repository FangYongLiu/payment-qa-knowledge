---
id: api_kyc_passport_init
object_type: API
domain: kyc
status: archived
owner: wiki-sync@acquire
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-20'
source_type: wiki
source_ref: confluence:PMDPayment/205914971
tags:
- passport
- init
- kyc
subdomain: passport
module: null
sensitivity: normal
name: 护照认证初始化接口
aliases:
- /kyc/passport/v1/init
related_services: []
related_tables: []
related_scenarios:
- kyc-passport-auth-flow
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
护照流程初始化，根据业务类型和业务数据创建认证流程，返回流程 token 及下一步骤指示。

## 路径/方法
- 路径：`/kyc/passport/v1/init`
- 说明：护照流程初始化

## 入参
业务请求：

| 名称 | 类型 | 非空 | 描述 | 样例 |
|---|---|---|---|---|
| bizType | String | Y | 业务类型，根据实际业务传入 | wps |
| bizData | String | Y | 业务数据，json格式 | {"employeeId":"100006201312","bufferInvalidTime":"2023-10-23"} |

## 出参
业务响应（非200则不返回）：

| 名称 | 类型 | 非空 | 描述 | 样例 |
|---|---|---|---|---|
| token | String | Y | 流程token | |
| nextStep | String | Y | 下一步骤：PP_OCR / PP_LIVENESS / AUDIT / DOWN | PP_OCR |
| tips | String | Y | 返回文案（如 nextStep 为 AUDIT 或 DOWN 时会返回文案） | |

## 错误码
- 非 200 则不返回业务响应（原文未列出具体错误码枚举）。

## 测试校验点
- 必填校验：bizType、bizData 缺失或为空时应拒绝。
- bizData 需为合法 JSON 格式，包含如 employeeId、bufferInvalidTime 等业务字段。
- 成功响应必须返回 token 与 nextStep。
- nextStep 取值仅在 {PP_OCR, PP_LIVENESS, AUDIT, DOWN} 范围内。
- 当 nextStep = AUDIT 或 DOWN 时，tips 字段应返回对应文案。
- 非 200 状态码下不应返回业务响应体。
- token 应可用于后续接口（submit-passport / liveness / submit-ocr）作为流程串联凭证。
