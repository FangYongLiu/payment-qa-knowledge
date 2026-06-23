---
id: api_kyc_passport_retake_selfie
object_type: API
domain: kyc
status: active
owner: xinwei.cao
reviewer: xinwei.cao
last_reviewed_at: '2026-06-20'
source_type: wiki
source_ref: wiki:e75788c0-8dcd-4b0c-95e3-8c08067ad9e7
tags:
- passport-kyc
- liveness
subdomain: passport-kyc
module: main
sensitivity: normal
name: 重拍自拍接口
aliases:
- Retake selfie
related_services:
- svc_kyc
---

## 用途
当 liveness（活体）认证失败时，用户选择重新拍摄自拍。调用此接口会重新启动 signzy kyc journey，让用户进入新的自拍流程。

## 路径/方法
- API: `/kyc/active-account/v1/passport/main/retake-selfie`
- Method: POST

## 入参
Request body (JSON):

| Parameter | Data Type | Mandatory | Example | Description |
|---|---|---|---|---|
| token | String | Y | 75762b77ed11445abd6078f739b53be7 | flow id |

## 出参
status=200 为成功。

Response body:

| Parameter | Data Type | Mandatory | Example | Description |
|---|---|---|---|---|
| commandType | String | Y | moveForward | tips: show tips；moveForward: go to the next step |
| commandData | json | Y | TipsInfo | 1, commandType = tips, return TipsInfo；2, commandType = moveForward, get next step |

commandData 示例（start signzy kyc journey）：
```json
{
  "commandType" : "moveForward",
  "commandData" : {
    "nextStep": "https://kyc-preproduction.signzy.app/pUwEHit",
    "data":{
      "token": "75762b77ed11445abd6078f739b53be7"
    }
  }
}
```

## 错误码
原文未提供该接口的具体业务错误码，仅约定 status=200 表示成功。

## 测试校验点
- 仅在 liveness 认证失败场景下被调用，前置条件为已存在有效 `token`（kyc flow id）。
- token 必填校验：缺失或非法 token 应被拒绝。
- 成功返回 `commandType=moveForward`，`commandData.nextStep` 为 signzy kyc journey URL，且 `commandData.data.token` 与请求 token 一致。
- 当返回 `commandType=tips` 时，前端应展示 TipsInfo（如 retakeTooManyFlag=Y 等限制场景）。
- 与 get-result 中 liveness fail 返回的 `redirectView` (viewName="Retake selfie") 链路衔接验证。
- 调用后应启动新的 signzy journey，与首次 start-journey 的下一步页面一致（nextStep 为 signzy URL）。
