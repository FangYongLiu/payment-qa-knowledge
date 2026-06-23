---
id: api_kyc_eid_renew_start_journey
object_type: API
domain: kyc
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-20'
source_type: wiki
source_ref: wiki:af2b7970-1661-4d20-90f7-3b86b8f72d58
tags:
- EID
- renew
- journey
subdomain: eid-renew
module: null
sensitivity: normal
name: 启动EID续期流程接口
aliases:
- start-journey
related_services: []
related_tables: []
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
start journey, create journey url。若用户已完成 journey，则返回结果（跳转 result 页面或 re-submit 页面）。

## 路径/方法
- API: `/kyc/active-account/v1/eid/renew/start-journey`
- Method: POST
- Domain:
  - SIM: https://sim.test2pay.com/cgs/api
  - UAT / PROD（同总览）
- 协议：JSON

## 入参
Request body：

| Parameter | Data Type | Mandatory | Example | Description |
|---|---|---|---|---|
| redirectUrl | String | N |  | Callback url |

## 出参
status=200 表示成功。

| Parameter | Data Type | Mandatory | Example | Description |
|---|---|---|---|---|
| commandType | String | Y | moveForward | tips: show tips；moveForward: go to the next step |
| commandData | json | Y |  | 1) commandType=tips → TipsInfo；2) commandType=moveForward → get next step |

commandData 三种典型返回：

1) start journey（跳转 signzy journey URL）
```
{
  "commandType" : "moveForward",
  "commandData" : {
    "nextStep": "https://kyc-preproduction.signzy.app/pUwEHit",
    "data":{ "token": "75762b77ed11445abd6078f739b53be7" }
  }
}
```

2) 用户已完成 journey → go to the result page
```
{
  "commandType" : "moveForward",
  "commandData" : {
    "nextStep": "route://native/kyc/result",
    "data":{ "token": "75762b77ed11445abd6078f739b53be7" }
  }
}
```

3) 用户已完成 journey → go to the reSubmit eid page
```
{
  "commandType" : "moveForward",
  "commandData" : {
    "nextStep": "route://native/kyc/re-submit",
    "data":{ "token": "75762b77ed11445abd6078f739b53be7" }
  }
}
```

## 错误码
原文未列出本接口具体错误码。

## 测试校验点
- 首次调用：返回 commandType=moveForward，nextStep 为 signzy journey URL，data.token 非空（后续接口的 flow id）。
- 用户已完成 journey 且需查看结果：nextStep=`route://native/kyc/result`，携带 token。
- 用户已完成 journey 且 OCR/信息需重提：nextStep=`route://native/kyc/re-submit`，携带 token。
- redirectUrl 非必填，未传也应正常返回。
- HTTP status=200 视为成功。
- token 透传：start-journey 返回的 token 应可被 get-result / confirm-info / submit-edit / retake-selfie / leave-submit / verify-again 使用。
