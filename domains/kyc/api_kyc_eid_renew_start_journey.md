---
id: api_kyc_eid_renew_start_journey
object_type: API
domain: kyc
status: active
owner: xinwei.cao
reviewer: xinwei.cao
last_reviewed_at: '2026-06-20'
source_type: wiki
source_ref: confluence:PMDPayment/1201700977
tags:
- eid-renew
- journey
- start
subdomain: active-account
module: eid-renew
sensitivity: normal
name: 启动EID续期Journey接口
aliases: []
related_services:
- svc_kyc
---

## 用途
启动EID续期journey，创建journey URL；如果用户已经完成过journey，则直接获取结果并跳转到对应页面（结果页 / re-submit页）。

## 路径/方法
- API：`/kyc/active-account/v1/eid/renew/start-journey`
- Method：POST

## 入参
Request body：

| Parameter | Data Type | Mandatory | Example | Description |
|---|---|---|---|---|
| redirectUrl | String | N | - | Callback url |

## 出参
status=200 表示成功。

| Parameter | Data Type | Mandatory | Example | Description |
|---|---|---|---|---|
| commandType | String | Y | moveForward | tips: show tips；moveForward: go to the next step |
| commandData | json | Y | - | 1）commandType=tips 时返回 TipsInfo；2）commandType=moveForward 时返回 next step |

commandData 三种典型场景：

1) start journey（进入signzy journey）
```
{
  "commandType":"moveForward",
  "commandData":{
    "nextStep":"https://kyc-preproduction.signzy.app/pUwEHit",
    "data":{"token":"75762b77ed11445abd6078f739b53be7"}
  }
}
```

2) go to result page
```
{
  "commandType":"moveForward",
  "commandData":{
    "nextStep":"route://native/kyc/result",
    "data":{"token":"75762b77ed11445abd6078f739b53be7"}
  }
}
```

3) go to reSubmit eid page
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
原文未列出专属错误码；以 status=200 表示成功，其他状态视为失败。

## 测试校验点
- 首次调用：返回 commandType=moveForward，nextStep 为 signzy journey URL，并下发 token。
- 用户已完成journey且需要查看结果：返回 nextStep=`route://native/kyc/result`，携带 token。
- 用户已完成journey且OCR信息需要修改：返回 nextStep=`route://native/kyc/re-submit`，携带 token。
- redirectUrl 非必填，缺省时不应阻塞流程。
- 返回的 token 后续应可用于 get-result / confirm-info / submit-edit / retake-selfie / leave-submit / verify-again 等接口。
