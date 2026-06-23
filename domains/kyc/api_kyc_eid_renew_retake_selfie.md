---
id: api_kyc_eid_renew_retake_selfie
object_type: API
domain: kyc
status: active
owner: xinwei.cao
reviewer: xinwei.cao
last_reviewed_at: '2026-06-20'
source_type: wiki
source_ref: wiki:af2b7970-1661-4d20-90f7-3b86b8f72d58
tags:
- eid-renew
- selfie
- liveness
subdomain: eid-renew
module: null
sensitivity: normal
name: 重拍自拍接口
aliases:
- Retake selfie
related_services:
- svc_kyc
---

## 用途
当活体认证(liveness authentication)失败时，用户选择重新拍摄自拍，重新发起 signzy kyc journey。

## 路径/方法
- API: `/kyc/active-account/v1/eid/renew/retake-selfie`
- Method: POST

## 入参
Request body：

| Parameter | Data Type | Mandatory | Example | Description |
|---|---|---|---|---|
| token | String | Y | 75762b77ed11445abd6078f739b53be7 | flow id |
| redirectUrl | String | N |  | Callback url |

## 出参
status=200 为成功

Response body：

| Parameter | Data Type | Mandatory | Example | Description |
|---|---|---|---|---|
| commandType | String | Y | moveForward | tips: show tips；moveForward: go to the next step |
| commandData | json | Y | TipsInfo | 1, commandType = tips, return TipsInfo；2, commandType = moveForward, get next step |

commandData 示例：

1、start signzy kyc journey
```json
{
  "commandType": "moveForward",
  "commandData": {
    "nextStep": "https://kyc-preproduction.signzy.app/pUwEHit",
    "data": {
      "token": "75762b77ed11445abd6078f739b53be7"
    }
  }
}
```

## 错误码
原文未提供专用错误码，仅以 status=200 表示成功。

## 测试校验点
- 仅在活体认证失败场景下触发本接口。
- 必传 token (flow id) 校验：缺失/无效 token 应失败。
- redirectUrl 为可选参数，传与不传均应可正常调用。
- 成功响应 status=200，且 commandType=moveForward，commandData.nextStep 为 signzy journey url，commandData.data.token 与请求 token 一致。
- 当 commandType=tips 时，应正确返回 TipsInfo 并由前端展示。
- 校验接口与 get-result 中 `retakeTooManyFlag=Y` 场景的衔接（重拍次数过多时的限制行为，依业务实现）。
