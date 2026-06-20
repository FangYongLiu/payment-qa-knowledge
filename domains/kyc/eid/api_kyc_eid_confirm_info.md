---
id: api_kyc_eid_confirm_info
object_type: API
domain: kyc
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-20'
source_type: wiki
source_ref: confluence:PMDPayment/1089405294
tags:
- eid
- kyc
- confirm
subdomain: eid
module: main
sensitivity: normal
name: 确认EID信息接口
aliases:
- Confirm Eid information
related_services: []
related_tables: []
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
用户对 EID 信息进行确认（不允许修改）。该接口不会进入人工审核流程。若用户未对 EID 信息做任何修改，可直接通过此接口完成确认。

## 路径/方法
- API: `/kyc/active-account/v1/eid/main/confirm-info`
- Method: `POST`

## 入参
Request body：

| 参数 | 类型 | 必填 | 示例 | 描述 |
|---|---|---|---|---|
| token | String | Y | 75762b77ed11445abd6078f739b53be7 | kyc flow id |
| industry | String | Y | High Value Goods Dealers | 用户选择的行业信息 |

## 出参
Response body：

| 参数 | 类型 | 必填 | 示例 | 描述 |
|---|---|---|---|---|
| commandType | String | Y | tips | tips: show tips；moveForward: go to the next step / action |
| commandData | json | Y | TipsInfo 结构 | commandType=tips 返回 TipsInfo；commandType=moveForward 返回 next step |

commandData 示例：

1. kyc fail
```
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
```
{
  "commandType":"tips",
  "commandData": {
      "type": "Page",
      "title": "Kyc complete",
      "tipText": "Your will active wallet account",
      "tipImg": "https://sim-m.test2pay.com/xxxxx/logo.png"
  }
}
```

3. kyc success
```
{
  "commandType":"moveForward",
  "commandData": {
      "type": "Popup",
      "title": "Kyc success",
      "tipText": "Kyc success",
      "tipImg": "https://sim-m.test2pay.com/xxxxx/logo.png"
  }
}
```

4. Change mobile
```
{
  "commandType": "moveForward",
  "commandData": {
      "nextStep": "/kyc/choose-account",
      "data": [
          {"walletId":"1223234455","balance":"100.00","mobileNo":"+971-54*****32","isLock":"N","id":"12232455"},
          {"walletId":"1223234455","balance":"0.00","mobileNo":"+971-56*****31","isLock":"Y","id":"12232456"}
      ]
  }
}
```

## 错误码
原文未给出具体错误码定义。

## 测试校验点
- token 必填，需为有效的 kyc flow id。
- industry 必填，应为 `inquire-industry` 接口返回的行业 value。
- 调用本接口后不进入人工审核流程；用户未修改 EID 信息时使用本接口完成确认。
- commandType=tips 时（kyc fail / kyc process）正确返回 TipsInfo（type/title/tipText/tipImg）。
- commandType=moveForward 时返回 kyc success 弹窗（type=Popup）或跳转 `/kyc/choose-account` 并返回钱包列表（walletId/balance/mobileNo/isLock/id）。
- 校验 Change mobile 场景下返回的多个 wallet 数据结构与 isLock 标识。
