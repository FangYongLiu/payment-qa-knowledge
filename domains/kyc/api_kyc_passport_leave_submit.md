---
id: api_kyc_passport_leave_submit
object_type: API
domain: kyc
status: active
owner: xinwei.cao
reviewer: xinwei.cao
last_reviewed_at: '2026-06-20'
source_type: wiki
source_ref: confluence:PMDPayment/1446215797
tags:
- POST
- kyc
- passport
subdomain: passport_kyc
module: active-account
sensitivity: normal
name: 放弃KYC接口
aliases:
- Leave kyc
- leave-submit
related_services:
- svc_kyc
related_tables: []
related_scenarios: []
---

## 用途
当用户放弃KYC时，记录用户放弃的原因。提交后不允许重新提交。前端无需校验该API的响应。

## 关联关系
- **所属服务**:[[svc_kyc]](related_services;api→service 边)
- **读写的表**:待补
- **被哪些场景测**:§9 登录/KYC 回归(待补具体 scenario 对象)

## 路径/方法
- 路径：`/kyc/active-account/v1/passport/main/leave-submit`
- Method：POST

## 入参
Request body (JSON)：

| Parameter | Data Type | Mandatory | Example | Description |
|---|---|---|---|---|
| token | String | Y | 75762b77ed11445abd6078f739b53be7 | flow id |
| reason | String | Y | I'm not comfortable sharing my lD | leave reason |

## 出参
Response body：原文未给出具体字段。说明：前端不需要验证该API的响应。

## 错误码
原文未给出。

## 测试校验点
- 必填校验：`token`、`reason` 缺失或为空时应拒绝。
- `token` 必须为有效的 flow id。
- 提交成功后，记录用户放弃KYC的原因。
- 提交后不允许再次提交（Resubmission is not allowed），需校验同一 flow 再次调用相关KYC接口的限制。
- 前端无需依赖响应内容，校验后端是否落库放弃原因。

参见：[[passport-kyc-s-model-api-overview]]、[[domain_kyc]]。
