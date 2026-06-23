---
id: api_kyc_eid_renew_verify_again
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
- kyc
- journey
subdomain: active-account
module: eid-renew
sensitivity: normal
name: 重新验证EID接口
aliases:
- Verify again
related_services:
- svc_kyc
---

## 用途
当 EID OCR 识别出的信息有误时，用户可重新验证，启动一个新的 journey。

## 路径/方法
- 路径：`/kyc/active-account/v1/eid/renew/verify-again`
- 方法：POST

## 入参
Request body：

| Parameter | Data Type | Mandatory | Example | Description |
|---|---|---|---|---|
| token | String | Y | 75762b77ed11445abd6078f739b53be7 | flow id |

## 出参
status=200 为成功。

Response body：

| Parameter | Data Type | Mandatory | Example | Description |
|---|---|---|---|---|
| commandType | String | Y | moveForward | tips: show tips；moveForward: go to the next step（action） |
| commandData | json | Y | TipsInfo | 1，commandType = tips, return TipsInfo；2，commandType = moveForward, get next step |

commandData 示例：

1、start signzy renew journey
```json
{
  "commandType" : "moveForward",
  "commandData" : {
    "nextStep": "/kyc/home"
  }
}
```

## 错误码
原文未列出。

## 测试校验点
- 必传 token 缺失或非法时，接口应拒绝处理。
- 仅在 EID OCR 信息有误的场景下允许调用，调用后应启动一个新的 journey。
- 成功响应 status=200，commandType=moveForward，commandData.nextStep=`/kyc/home`。
- commandType=tips 时，commandData 应返回 TipsInfo 结构（页面提示）。
- 与 `get-result` 返回的 reSubmit eid 流程衔接：在确认 OCR 信息有误后调用本接口可重新进入 journey。
