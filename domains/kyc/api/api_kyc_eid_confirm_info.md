---
id: api_kyc_eid_confirm_info
object_type: API
domain: kyc
status: active
owner: xinwei.cao
reviewer: xinwei.cao
last_reviewed_at: '2026-06-20'
source_type: wiki
source_ref: wiki:c77c6bdf-23d4-4c31-b325-128a8f8a6d3e
tags:
- EID
- KYC
- confirm
subdomain: eid
module: main
sensitivity: normal
name: 确认EID信息接口 (confirm-info)
aliases:
- confirm-info
related_services:
- svc_kyc
related_tables:
- tbl_kyc_tm_kyc_apply
- tbl_kyc_tr_biz_record_ica
- tbl_kyc_tr_biz_record_ocr
related_scenarios:
- scn_kyc_eid_full_journey
---

## 用途
用户确认 EID 信息（不修改），并提交所选 industry。该接口不会进入人工审核流程（This api will not be submitted for manual review）。

## 关联关系
- **所属服务**:[[svc_kyc]](related_services;api→service 边)
- **读写的表**:待补
- **被哪些场景测**:[[scn_kyc_eid_full_journey]]
- **被哪些自动化覆盖**:[[auto_kyc_eid_journey]]

## 路径/方法
- 路径：`/kyc/active-account/v1/eid/main/confirm-info`
- 方法：POST

## 入参
Request body：

| Parameter | Data Type | Mandatory | Example | Description |
|---|---|---|---|---|
| token | String | Y | 75762b77ed11445abd6078f739b53be7 | kyc flow id |
| industry | String | Y | High Value Goods Dealers | The industry information selected by the user |

## 出参
Response body：

| Parameter | Data Type | Mandatory | Example | Description |
|---|---|---|---|---|
| commandType | String | Y | tips | tips: show tips；moveForward: go to the next step；action |
| commandData | json | Y | TipsInfo 结构 | 1. commandType=tips → 返回 TipsInfo；2. commandType=moveForward → 返回下一步动作 |

返回示例：

1) kyc fail
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

2) kyc process
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

4) Change mobile
```json
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
原文未提供该接口专用错误码（依赖 commandType=tips 的失败场景文案，如 "Kyc fail, please retry"）。

## 测试校验点
- token、industry 必填校验；token 取自此前 KYC flow（如 inquire-info / get-result 返回的 token）。
- industry 取值需来自 inquire-industry 返回的 industryList[].value。
- 调用成功后**不进入人工审核**（区别于 submit-edit 修改场景）。
- 校验四类返回分支：kyc fail（tips Page）、kyc process（tips Page，文案 "Your will active wallet account"）、kyc success（moveForward Popup）、Change mobile（moveForward，nextStep=/kyc/choose-account 且返回钱包列表）。
- Change mobile 分支中 data 列表字段（walletId、balance、mobileNo、isLock、id）齐全。
- commandType 与 commandData 结构对应：tips → TipsInfo；moveForward → 含 nextStep/data 或 Popup 结构。
