---
id: api_kyc_passport_start_journey
object_type: API
domain: kyc
status: active
owner: xinwei.cao
reviewer: xinwei.cao
last_reviewed_at: '2026-06-20'
source_type: wiki
source_ref: confluence:PMDPayment/1446215797
tags:
- kyc
- passport
- journey
subdomain: passport_kyc
module: active-account
sensitivity: normal
name: 启动护照KYC旅程接口
aliases:
- start-journey
- Start Passport Kyc journey
related_services:
- svc_kyc
---

## 用途
启动护照KYC旅程，创建journey URL；若用户已完成journey，则直接返回结果（跳转结果页）。

## 路径/方法
- API: `/kyc/active-account/v1/passport/main/start-journey`
- Method: POST
- Domain: SIM `https://sim.test2pay.com/cgs/api`（UAT/PROD 见总览）

## 入参
Request body (JSON)：

| Parameter | Data Type | Mandatory | Example | Description |
|---|---|---|---|---|
| bizType | String | Y | wps | 业务类型 |
| employeeId | String | Y | 01JWDM22Z2FVNMVB180RQ0B010 | 员工ID |

## 出参
status=200 表示成功。Response body：

| Parameter | Data Type | Mandatory | Example | Description |
|---|---|---|---|---|
| commandType | String | Y | moveForward | tips: show tips；moveForward: go to the next step |
| commandData | json | Y | - | commandType=tips 时返回 TipsInfo；commandType=moveForward 时返回 next step |

commandData 示例：

1) 未做过kyc，启动journey：
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

2) 已完成journey，跳转结果页：
```json
{
  "commandType" : "moveForward",
  "commandData" : {
    "nextStep": "route://native/kyc/result",
    "data":{
      "token": "75762b77ed11445abd6078f739b53be7"
    }
  }
}
```

## 错误码
原文未列明具体错误码；以 status=200 判定成功，非200可能伴随 commandType=tips 的提示信息（TipsInfo）。

## 测试校验点
- bizType、employeeId 为必填，缺失时校验失败。
- 首次发起KYC：返回 commandType=moveForward，nextStep 为外部 signzy journey URL，data.token 非空，后续接口（get-result/confirm-info/retake-selfie/verify-again/leave-submit）需复用该 token。
- 用户已完成journey再次调用：返回 commandType=moveForward，nextStep=`route://native/kyc/result`，并携带 data.token。
- 校验响应 status=200 表示成功。
- 验证 token 在不同分支下均能正确生成并透传至 [[api_kyc_passport_get_result]]。
