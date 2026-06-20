---
id: api_kyc_eid_submit_edit
object_type: API
domain: kyc
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-20'
source_type: wiki
source_ref: confluence:PMDPayment/1089405294
tags:
- EID
- KYC
- manual-review
subdomain: eid
module: main
sensitivity: normal
name: 提交编辑后EID信息接口
aliases:
- Submit Eid information
related_services: []
related_tables: []
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
用户确认修改后的 EID 信息后调用本接口提交。当用户对 EID 信息做了修改时，将进入人工审核阶段；若用户未做任何修改，则不需要人工审核。

## 路径/方法
- API：`/kyc/active-account/v1/eid/main/submit-edit`
- Method：POST

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
| commandType | String | Y | tips | tips: show tips；moveForward: go to the next step；action |
| commandData | json | Y | TipsInfo | 1）commandType=tips，返回 TipsInfo；2）commandType=moveForward，进入下一步 |

响应示例：

1) kyc fail
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

2) kyc process
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

3) kyc success
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
原文未列出。

## 测试校验点
- 必填字段 token / idNumber / name / birthDate / expiryDate / industry 缺失时校验失败。
- idNumber、name 须以密文（Ciphertext）形式提交。
- birthDate、expiryDate 必须符合 yyyy-MM-dd 格式。
- 用户对 EID 信息做了修改时，提交后流程应进入人工审核（kyc process 分支）。
- 用户未做任何修改时不应进入人工审核。
- 响应 commandType 应在 tips / moveForward / action 中取值，对应分支：kyc fail（tips）、kyc process（tips）、kyc success（moveForward + Popup）。
