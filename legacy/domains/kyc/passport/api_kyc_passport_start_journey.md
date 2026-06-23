---
id: api_kyc_passport_start_journey
object_type: API
domain: kyc
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-20'
source_type: wiki
source_ref: wiki:e75788c0-8dcd-4b0c-95e3-8c08067ad9e7
tags:
- passport
- kyc
- start-journey
subdomain: passport
module: active-account
sensitivity: normal
name: 启动Passport KYC旅程接口
aliases: []
related_services: []
related_tables: []
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
启动 Passport KYC 旅程，创建 journey URL；若用户已经执行过 journey，则直接获取结果（跳转到结果页）。

## 路径/方法
- 路径：`/kyc/active-account/v1/passport/main/start-journey`
- Method：POST
- Domain：
  - SIM：`https://sim.test2pay.com/cgs/api`
  - UAT / PROD：见环境配置

## 入参
Request body（JSON）：

| Parameter | Data Type | Mandatory | Example | Description |
|---|---|---|---|---|
| bizType | String | Y | wps | 业务类型 |
| employeeId | String | Y | 01JWDM22Z2FVNMVB180RQ0B010 | 员工ID |

## 出参
status=200 表示成功。

Response body：

| Parameter | Data Type | Mandatory | Example | Description |
|---|---|---|---|---|
| commandType | String | Y | moveForward | tips: show tips；moveForward: go to the next step |
| commandData | json | Y | - | 1. commandType = tips → 返回 TipsInfo；2. commandType = moveForward → 返回 next step |

commandData 示例：

1）尚未进行 KYC，启动 journey：
```json
{
  "commandType": "moveForward",
  "commandData": {
    "nextStep": "https://kyc-preproduction.signzy.app/pUwEHit",
    "data": { "token": "75762b77ed11445abd6078f739b53be7" }
  }
}
```

2）已完成，跳转结果页：
```json
{
  "commandType": "moveForward",
  "commandData": {
    "nextStep": "route://native/kyc/result",
    "data": { "token": "75762b77ed11445abd6078f739b53be7" }
  }
}
```

## 错误码
原文未提供具体错误码定义；以 status=200 表示成功，否则视为失败。

## 测试校验点
- bizType、employeeId 必填校验。
- 用户首次进入：`commandType=moveForward`，`commandData.nextStep` 为外部 signzy journey URL，且返回 `data.token`。
- 用户已完成 journey：`commandType=moveForward`，`commandData.nextStep=route://native/kyc/result`，且返回 `data.token`。
- 返回的 token 可用于后续 `get-result` / `confirm-info` / `retake-selfie` / `verify-again` / `leave-submit` 接口（参见 [[api_kyc_passport_get_result]]）。
- status=200 视为成功响应。
