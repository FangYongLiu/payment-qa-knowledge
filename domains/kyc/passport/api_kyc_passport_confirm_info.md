---
id: api_kyc_passport_confirm_info
object_type: API
domain: kyc
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-20'
source_type: wiki
source_ref: confluence:PMDPayment/1446215797
tags:
- passport
- kyc
- confirm
subdomain: passport
module: active-account
sensitivity: normal
name: 确认护照信息接口
aliases: []
related_services: []
related_tables: []
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
用户确认OCR识别出的护照信息（不可修改）。该接口不会提交人工审核，根据后端KYC流程当前状态返回 tips 或 moveForward 指令。

## 路径/方法
- 路径：`/kyc/active-account/v1/passport/main/confirm-info`
- 方法：POST

## 入参
Request body：

| Parameter | Data Type | Mandatory | Example | Description |
|---|---|---|---|---|
| token | String | Y | 75762b77ed11445abd6078f739b53be7 | kyc flow id |

## 出参
Response body：

| Parameter | Data Type | Mandatory | Example | Description |
|---|---|---|---|---|
| commandType | String | Y | tips | tips: show tips；moveForward: go to the next step |
| commandData | json | Y | TipsInfo 结构 | 1. commandType=tips 返回 TipsInfo；2. commandType=moveForward 返回 next step |

返回示例：

1. kyc fail
```json
{
  "commandType":"tips",
  "commandData": {
      "type": "Page",
      "title": "Kyc fail",
      "tipText": "Kyc fail, please retry",
      "tipImg": "https://sim-m.test2pay.com/xxxxx/logo.png"
  }
}
```

2. kyc process
```json
{
  "commandType":"tips",
  "commandData": {
      "type": "Page",
      "title": "Kyc complete",
      "tipText": "We are verifying your account",
      "tipImg": "https://sim-m.test2pay.com/xxxxx/logo.png"
  }
}
```

3. kyc success
```json
{
  "commandType":"moveForward",
  "commandData": {
      "type": "Popup",
      "title": "Kyc success",
      "tipText": "Your account has actived.",
      "tipContent": "You need to upload your Emirates lD copy before Nov. 15,2023 to continue using your account",
      "tipImg": "https://sim-m.test2pay.com/xxxxx/logo.png"
  }
}
```

## 错误码
原文未提供该接口的具体错误码定义。

## 测试校验点
- 请求必须携带有效 token（kyc flow id），缺失或非法时应返回错误。
- 调用确认后，用户不可修改护照信息。
- 该接口不会触发人工审核流程。
- 校验三类返回分支：
  - kyc fail → commandType=tips，type=Page，提示 "Kyc fail, please retry"。
  - kyc process → commandType=tips，type=Page，提示 "We are verifying your account"。
  - kyc success → commandType=moveForward，type=Popup，提示账户已激活，并包含 tipContent 关于 Emirates ID 上传的说明。
- 当 commandType=tips 时，commandData 应为 TipsInfo 结构（含 type/title/tipText/tipImg 等）。
- 当 commandType=moveForward 时，前端应跳转到下一步。
