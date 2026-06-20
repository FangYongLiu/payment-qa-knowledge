---
id: api_kyc_passport_leave_submit
object_type: API
domain: kyc
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-20'
source_type: wiki
source_ref: wiki:e75788c0-8dcd-4b0c-95e3-8c08067ad9e7
tags:
- passport
- kyc
- leave
subdomain: passport
module: active-account
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
当用户放弃 KYC 时，记录用户放弃的原因。提交后不允许再次提交。前端无需校验该接口的响应。

## 路径/方法
- API: `/kyc/active-account/v1/passport/main/leave-submit`
- Method: POST

## 入参
Request body：

| Paramters | Data Type | Mandatory | Example | Description |
|---|---|---|---|---|
| token | String | Y | 75762b77ed11445abd6078f739b53be7 | flow id |
| reason | String | Y | I'm not comfortable sharing my lD | leave reason |

## 出参
Response body：原文未给出具体字段，且说明前端不需要校验该 API 的响应。

## 错误码
原文未提供。

## 测试校验点
- token 必填，需为有效的 kyc flow id。
- reason 必填，记录用户放弃原因。
- 提交后该 flow 不允许再次提交（验证重复提交被拒绝）。
- 前端不依赖该接口响应即可继续后续流程。

参见 [[passport-kyc-s-model-api-overview]]。
