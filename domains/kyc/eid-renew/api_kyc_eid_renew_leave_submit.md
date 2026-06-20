---
id: api_kyc_eid_renew_leave_submit
object_type: API
domain: kyc
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-20'
source_type: wiki
source_ref: confluence:PMDPayment/1201700977
tags:
- eid-renew
- kyc
- leave
subdomain: eid-renew
module: null
sensitivity: normal
name: 放弃KYC接口
aliases:
- Leave kyc
related_services: []
related_tables: []
related_scenarios:
- eid-renew-flow-overview
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
当用户放弃 KYC 续期时，记录用户放弃原因。提交后不允许再次提交（Resubmission is not allowed）。前端无需校验该 API 的响应。

## 路径/方法
- 路径：`/kyc/active-account/v1/eid/renew/leave-submit`
- Method：POST
- 协议：JSON

## 入参
Request body：

| Parameter | Data Type | Mandatory | Example | Description |
|---|---|---|---|---|
| token | String | Y | 75762b77ed11445abd6078f739b53be7 | flow id |
| reason | String | Y | I'm not comfortable sharing my lD | leave reason（放弃原因） |

## 出参
Response body：原文未列具体字段（前端无需校验响应）。

## 错误码
原文未列出。

## 测试校验点
- 必填校验：token、reason 必传。
- 提交后 flow 标记为放弃，再次调用提交类接口（如 confirm-info / submit-edit）应被拒绝（Resubmission is not allowed）。
- 前端流程：调用该接口后不依赖响应内容继续走放弃流程。
- 后端记录 reason 文本（如 "I'm not comfortable sharing my lD"）落库可追溯。
