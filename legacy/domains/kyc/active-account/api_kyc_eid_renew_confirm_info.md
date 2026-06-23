---
id: api_kyc_eid_renew_confirm_info
object_type: API
domain: kyc
status: archived
owner: wiki-sync@acquire
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-20'
source_type: wiki
source_ref: confluence:PMDPayment/1201700977
tags:
- eid-renew
- kyc
- confirm
subdomain: active-account
module: eid-renew
sensitivity: normal
name: 确认EID信息接口
aliases:
- Confirm Eid information
related_services: []
related_tables: []
related_scenarios:
- eid-renew-flow-overview
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
用户确认 EID 信息(不可修改)。该接口不会进入人工审核(manual review)阶段。用于 EID 续期流程中，用户对 OCR 出的 EID 信息无修改时确认提交，并附带行业(industry)信息。

## 路径/方法
- API: `/kyc/active-account/v1/eid/renew/confirm-info`
- Method: `POST`
- Domain:
  - SIM: `https://sim.test2pay.com/cgs/api`
  - UAT: (未提供)
  - PROD: (未提供)

## 入参
Request body (JSON):

| Parameter | Data Type | Mandatory | Example | Description |
|---|---|---|---|---|
| token | String | Y | 75762b77ed11445abd6078f739b53be7 | kyc flow id |
| industry | String | Y | High Value Goods Dealers | 用户选择的行业信息 |

## 出参
Response body (status=200 表示成功):

| Parameter | Data Type | Mandatory | Example | Description |
|---|---|---|---|---|
| commandType | String | Y | tips | `tips`: show tips；`moveForward`: go to the next step |
| commandData | json | Y | TipsInfo 结构 | 1) commandType=tips 返回 TipsInfo；2) commandType=moveForward 返回 next step |

示例 commandData：

1) renew fail
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

2) renew process
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

3) renew success
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

## 错误码
原文未列出具体错误码；通过 `commandType=tips` + `commandData` 中 `title/tipText` 表达失败/进行中状态(如 "Kyc fail")。

## 测试校验点
- token 必填，且与 EID 续期 journey 一致；缺失/非法时应失败。
- industry 必填，传入用户选择值(如 `High Value Goods Dealers`)。
- 该接口不进入人工审核流程(无修改场景)。
- 出参三种典型分支均能正确返回：
  - renew fail → `commandType=tips`，type=Page，title=`Kyc fail`。
  - renew process → `commandType=tips`，type=Page，title=`Kyc complete`，提示将激活钱包账户。
  - renew success → `commandType=moveForward`，type=Popup，title=`Kyc success`。
- 与 `submit-edit` 区分：confirm-info 不修改 EID 字段，仅提交 token+industry，不触发人工审核。
