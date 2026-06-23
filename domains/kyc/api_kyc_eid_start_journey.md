---
id: api_kyc_eid_start_journey
object_type: API
domain: kyc
status: active
owner: xinwei.cao
reviewer: xinwei.cao
last_reviewed_at: '2026-06-20'
source_type: wiki
source_ref: wiki:c77c6bdf-23d4-4c31-b325-128a8f8a6d3e
tags:
- kyc
- eid
- journey
subdomain: eid
module: main
sensitivity: normal
name: 启动EID KYC Journey接口 (start-journey)
aliases:
- start-journey
related_services:
- svc_kyc
---

## 用途
启动EID KYC journey，创建journey URL；如果用户已经执行过journey，则直接返回结果（用于跳转到结果页/重提交EID页等）。

## 路径/方法
- API: `/kyc/active-account/v1/eid/main/start-journey`
- Method: POST

## 入参
Request body：

| Parameter | Data Type | Mandatory | Example | Description |
|---|---|---|---|---|
| redirectUrl | String | N | | Callback url |

## 出参
status=200 表示成功

| Parameter | Data Type | Mandatory | Example | Description |
|---|---|---|---|---|
| commandType | String | Y | moveForward | tips: show tips；moveForward: go to the next step；action |
| commandData | json | Y | | 1. commandType=tips 返回 TipsInfo；2. commandType=moveForward 返回下一步 |

commandData 场景示例：

1. 未做过kyc，启动journey（HTTP mode）
```
{
  "commandType":"moveForward",
  "commandData":{
    "nextStep":"https://kyc-preproduction.signzy.app/pUwEHit",
    "mode":"HTTP",
    "data":{"token":"75762b77ed11445abd6078f739b53be7"}
  }
}
```

2. 未做过kyc，启动journey（TOKEN mode）
```
{
  "commandType":"moveForward",
  "commandData":{
    "nextStep":"f62e1102-eea5-4762-ba0b-a9b19750472c",
    "mode":"TOKEN",
    "data":{"token":"75762b77ed11445abd6078f739b53be7"}
  }
}
```

3. 跳转到结果页
```
{
  "commandType":"moveForward",
  "commandData":{
    "nextStep":"route://native/kyc/result",
    "data":{"token":"75762b77ed11445abd6078f739b53be7"}
  }
}
```

4. 跳转到重提交EID页
```
{
  "commandType":"moveForward",
  "commandData":{
    "nextStep":"route://native/kyc/re-submit",
    "data":{"token":"75762b77ed11445abd6078f739b53be7"}
  }
}
```

## 错误码
原文未提供具体错误码定义；status=200 视为成功。

## 测试校验点
- 用户未做过KYC时，返回 commandType=moveForward，commandData.nextStep 为 signzy journey URL，且 mode 为 HTTP 或 TOKEN，data.token 非空。
- 用户已完成journey时，nextStep 应为 `route://native/kyc/result`，并带回 token。
- 处于需要重提交EID的状态时，nextStep 应为 `route://native/kyc/re-submit`，并带回 token。
- redirectUrl 非必填，当传入时回调流程应能跳回指定地址。
- 返回的 token 与后续 get-result / confirm-info / submit-edit / retake-selfie / leave-submit / verify-again 接口使用的 flow id 保持一致。
- mode=HTTP 时 nextStep 为可访问的 https URL；mode=TOKEN 时 nextStep 为 token 字符串（由前端组装）。
