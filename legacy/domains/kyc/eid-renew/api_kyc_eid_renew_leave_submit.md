---
id: api_kyc_eid_renew_leave_submit
object_type: API
domain: kyc
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-20'
source_type: wiki
source_ref: wiki:af2b7970-1661-4d20-90f7-3b86b8f72d58
tags:
- eid-renew
- leave
subdomain: eid-renew
module: null
sensitivity: normal
name: 放弃KYC接口
aliases:
- Leave kyc
related_services: []
related_tables: []
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
当用户放弃KYC流程时，记录用户放弃的原因。Resubmission is not allowed（不允许重新提交）。前端无需校验该API的响应。

## 路径/方法
- API: `/kyc/active-account/v1/eid/renew/leave-submit`
- Method: POST

## 入参
Request body：

| Parameter | Data Type | Mandatory | Example | Description |
|---|---|---|---|---|
| token | String | Y | 75762b77ed11445abd6078f739b53be7 | flow id |
| reason | String | Y | I'm not comfortable sharing my ID | leave reason |

## 出参
Response body：原文未列出具体字段（前端不需要校验该API的response）。

## 错误码
原文未提供。

## 测试校验点
- token 必传，且为有效的 kyc flow id。
- reason 必传，记录用户放弃原因（如 "I'm not comfortable sharing my ID"）。
- 调用成功后，用户不允许再重新提交 KYC（Resubmission is not allowed）。
- 前端无需依赖此接口的响应内容做后续判断。
