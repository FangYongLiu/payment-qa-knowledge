---
id: api_kyc_check_reminder
object_type: API
domain: kyc
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-20'
source_type: wiki
source_ref: confluence:PMDPayment/1089405294
tags:
- kyc
- reminder
- eid
subdomain: eid-kyc
module: active-account
sensitivity: normal
name: KYC状态提醒接口
aliases:
- KYC Reminder
- check-reminder
related_services: []
related_tables: []
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
检查用户 KYC 状态。当用户已完成 KYC 流程并处于待确认（waiting confirm）状态时，通过该接口提醒用户尽快确认 EID 信息（confirm the Eid information ASAP）。

## 路径/方法
- API：`/kyc/active-account/v1/kyc/check-reminder`
- Method：`POST`
- 协议：JSON

## 入参
Request body：

| 参数 | 类型 | 必填 | 示例 | 描述 |
|---|---|---|---|---|
| scene | String | Y | BOTIM_MONEY | Definition source（场景标识） |

## 出参
Response body：

| 参数 | 类型 | 必填 | 示例 | 描述 |
|---|---|---|---|---|
| reminderType | String | Y | KYC_CONFIRM | Reminder type，例：KYC_CONFIRM |
| reminderMsg | String | Y | xxxxxx | description content（提醒描述内容） |
| icon | String | N | https://xxxxx | The picture of the page（页面图标） |
| link | String | N | https://xxxxx | Click on the link that redirects（点击跳转的链接） |
| token | String | N | 75762b77ed11445abd6078f739b53be7 | KYC flow id |

## 错误码
原文未提供本接口具体错误码定义。

## 测试校验点
- 入参 `scene` 必传，验证不同场景值（如 BOTIM_MONEY）下返回的 reminder 内容是否正确。
- 当用户已完成 KYC 流程且处于 waiting confirm 状态时，应返回 `reminderType=KYC_CONFIRM` 且 `reminderMsg` 非空。
- 校验 `token` 与当前 KYC flow id 一致，可用于后续 confirm-info / submit-edit 等接口。
- 可选字段 `icon`、`link` 在不同场景下的返回与展示是否符合预期。
- 当用户未处于待确认状态时，接口返回内容应符合"无需提醒"的业务约定（原文未细化，需结合业务确认）。
