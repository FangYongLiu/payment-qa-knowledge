---
id: api_kyc_passport_init
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
- init
subdomain: passport
module: null
sensitivity: normal
name: 护照认证初始化接口
aliases:
- /kyc/passport/v1/init
related_services: []
related_tables: []
related_scenarios:
- passport-kyc-flow
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
护照流程初始化，启动护照认证流程并返回流程 token 与下一步骤指示。

## 路径/方法
- 路径：`/kyc/passport/v1/init`
- 方法：原文未注明（业务请求/响应形式）

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
原文未明确列出，仅说明：非200则不返回业务响应字段。

## 测试校验点
- bizType、bizData 必填校验，bizData 需为合法 JSON（含 employeeId、bufferInvalidTime 等字段）。
- 成功响应必须返回 token 与 nextStep。
- nextStep 取值需在 {PP_OCR, PP_LIVENESS, AUDIT, DOWN} 范围内。
- 当 nextStep = AUDIT 或 DOWN 时，tips 文案需返回且非空。
- 非200状态下不应返回业务响应字段。
