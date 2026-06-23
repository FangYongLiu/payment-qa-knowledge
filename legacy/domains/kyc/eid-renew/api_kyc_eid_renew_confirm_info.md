---
id: api_kyc_eid_renew_confirm_info
object_type: API
domain: kyc
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-20'
source_type: wiki
source_ref: wiki:af2b7970-1661-4d20-90f7-3b86b8f72d58
tags:
- eid-renew
- kyc
- confirm
subdomain: eid-renew
module: null
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
用户确认 EID 信息（不可修改），同时提交所选行业信息。该接口不会进入人工审核。

## 路径/方法
- 路径：`/kyc/active-account/v1/eid/renew/confirm-info`
- 方法：POST

## 入参
| Parameter | Data Type | Mandatory | Example | Description |
|---|---|---|---|---|
| token | String | Y | 75762b77ed11445abd6078f739b53be7 | kyc flow id |
| industry | String | Y | High Value Goods Dealers | The industry information selected by the user |

## 出参
| Parameter | Data Type | Mandatory | Example | Description |
|---|---|---|---|---|
| commandType | String | Y | tips | tips: show tips；moveForward: go to the next step |
| commandData | json | Y | TipsInfo 结构 | commandType=tips 返回 TipsInfo；commandType=moveForward 返回 next step |

响应示例：

1. renew fail
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

2. renew process
```json
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
原文未列出特定错误码；status=200 视为成功（参照同组接口约定）。

## 测试校验点
- token、industry 为必填，缺失/无效应返回失败。
- 调用本接口后不应触发人工审核流程（与 submit-edit 区分）。
- commandType 仅可能为 tips 或 moveForward；commandData 结构需与 commandType 匹配（TipsInfo 或 next step）。
- renew fail 场景返回 type=Page，标题 "Kyc fail"。
- renew process 场景返回 type=Page，标题 "Kyc complete"，提示将激活钱包账户。
- renew success 场景返回 commandType=moveForward，type=Popup，标题 "Kyc success"。
- 用户在该步骤不可修改 EID 信息，仅做确认。
