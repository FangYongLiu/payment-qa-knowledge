---
id: api_kyc_eid_renew_submit_edit
object_type: API
domain: kyc
status: active
owner: xinwei.cao
reviewer: xinwei.cao
last_reviewed_at: '2026-06-20'
source_type: wiki
source_ref: wiki:af2b7970-1661-4d20-90f7-3b86b8f72d58
tags:
- eid
- renew
- kyc
- manual-review
subdomain: eid-renew
module: null
sensitivity: normal
name: 提交修改后EID信息接口
aliases: []
related_services:
- svc_kyc
---

## 用途
用户确认修改后的 EID 信息后调用本接口提交。当用户修改了 EID 信息时，将进入人工审核阶段；若用户未做任何修改，则无需人工审核。

## 路径/方法
- API: `/kyc/active-account/v1/eid/renew/submit-edit`
- Method: POST

## 入参
Request body：

| Parameter | Data Type | Mandatory | Example | Description |
|---|---|---|---|---|
| token | String | Y | 75762b77ed11445abd6078f739b53be7 | flow id |
| idNumber | String | Y | 784XXXXXXXXXXX | EID number（Ciphertext） |
| name | String | Y | San zhan | name（Ciphertext） |
| birthDate | Date | Y | 1992-01-01 | format：yyyy-MM-dd |
| expiryDate | Date | Y | 2026-12-01 | format：yyyy-MM-dd |
| industry | String | Y | High Value Goods Dealers | The industry information selected by the user |

## 出参
Response body：

| Parameter | Data Type | Mandatory | Example | Description |
|---|---|---|---|---|
| commandType | String | Y | tips | tips: show tips；moveForward: go to the next step（action） |
| commandData | json | Y | TipsInfo | 1. commandType=tips, return TipsInfo；2. commandType=moveForward, get next step |

响应示例：

1. renew fail
```json
{
  "commandType":"tips",
  "commandData": {
    "type": "Page",
    "title": "Kyc fail",
    "tipText": "Kyc fail, please retry",
    "tipImg": "https://sim-m.test2pay.com/xxxxx/logo.png",
    "redirectView":[
      {"viewName":"Try again","viewType":"default","viewUrl":"https://xxx.com"},
      {"viewName":"Contact us","viewType":"default","viewUrl":"https://xxx.com"}
    ]
  }
}
```

2. renew process
```json
{
  "commandType":"tips",
  "commandData": {
    "type": "Page",
    "title": "Kyc complete",
    "tipText": "Your will active wallet account",
    "tipImg": "https://sim-m.test2pay.com/xxxxx/logo.png",
    "redirectView":[
      {"viewName":"Okay","viewType":"default","viewUrl":"https://xxx.com"}
    ]
  }
}
```

3. renew success
```json
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

## 错误码
原文未提供具体错误码（status=200 表示成功，依据总览约定）。

## 测试校验点
- token 必填校验，必须为有效的 flow id。
- idNumber、name 必须为 RSA 密文（Ciphertext）传输。
- birthDate、expiryDate 必须符合 yyyy-MM-dd 格式。
- industry 必填，使用用户选择的行业信息。
- 用户修改了 EID 信息时，提交后应进入人工审核（renew process 分支，commandType=tips，title="Kyc complete"）。
- 用户未修改任何信息时，无需人工审核，可直接 renew success（commandType=moveForward, type=Popup）。
- renew fail 场景需返回 redirectView 中的 "Try again" 与 "Contact us" 入口。
- renew process 场景需返回 redirectView 中的 "Okay" 入口。
- 与 confirm-info 接口区分：本接口处理"修改后"的 EID 信息提交，可能触发人工审核；confirm-info 不进入人工审核。
