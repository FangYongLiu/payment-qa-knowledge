---
id: api_kyc_eid_leave_submit
object_type: API
domain: kyc
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-20'
source_type: wiki
source_ref: confluence:PMDPayment/1089405294
tags:
- EID
- KYC
- leave
subdomain: eid
module: main
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
当用户放弃 KYC 时，记录用户放弃的原因。放弃后不允许重新提交。前端无需校验该接口的响应。

## 路径/方法
- API: `/kyc/active-account/v1/eid/main/leave-submit`
- Method: POST

## 入参
Request body:

| Parameter | Data Type | Mandatory | Example | Description |
|---|---|---|---|---|
| token | String | Y | 75762b77ed11445abd6078f739b53be7 | flow id |
| reason | String | Y | I'm not comfortable sharing my lD | leave reason |

## 出参
Response body: 原文未列出具体字段（前端无需验证该接口响应）。

## 错误码
原文未提供。

## 测试校验点
- token 必填，需为有效的 KYC flow id。
- reason 必填，能正确记录用户放弃原因。
- 调用成功后，该 flow 不允许 Resubmission（不允许重新提交）。
- 前端不依赖 response 内容，接口需保证幂等/容错记录。
