---
id: api_kyc_passport_retake_selfie
object_type: API
domain: kyc
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-20'
source_type: wiki
source_ref: confluence:PMDPayment/1446215797
tags:
- passport-kyc
- liveness
subdomain: passport-kyc
module: active-account
sensitivity: normal
name: 重新自拍接口
aliases:
- Retake selfie
related_services: []
related_tables: []
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
当 liveness 活体认证失败后，用户选择重新发起自拍流程，调用该接口启动新的 signzy kyc journey。

## 路径/方法
- API: `/kyc/active-account/v1/passport/main/retake-selfie`
- Method: POST
- Domain:
  - SIM: https://sim.test2pay.com/cgs/api
  - UAT: (未提供)
  - PROD: (未提供)
- 协议：JSON

## 入参
Request body：

| Parameter | Data Type | Mandatory | Example | Description |
|---|---|---|---|---|
| token | String | Y | 75762b77ed11445abd6078f739b53be7 | flow id |

## 出参
Response body（status=200 为成功）：

| Parameter | Data Type | Mandatory | Example | Description |
|---|---|---|---|---|
| commandType | String | Y | moveForward | tips: show tips；moveForward: go to the next step |
| commandData | json | Y | TipsInfo | 1) commandType=tips → 返回 TipsInfo；2) commandType=moveForward → 获取下一步 |

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
原文未列出该接口的具体错误码，仅给出 status=200 表示成功。

## 测试校验点
- 仅在 liveness 活体认证失败场景下允许触发该接口。
- 入参 token 必填，需为合法的 kyc flow id。
- status=200 视为成功；返回 commandType 取值仅 tips / moveForward 两类。
- 当 commandType=moveForward 时，commandData.nextStep 应为 signzy kyc journey URL，且 commandData.data.token 与请求 token 保持一致。
- 当 commandType=tips 时，commandData 应符合 TipsInfo 结构。
- 与 get-result 返回的 liveness fail（redirectView 中 viewName="Retake selfie"，retakeTooManyFlag）联动校验：retakeTooManyFlag=Y 时是否仍允许调用 retake-selfie 需关注。
