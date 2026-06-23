---
id: api_kyc_check_reminder
object_type: API
domain: kyc
status: active
owner: xinwei.cao
reviewer: xinwei.cao
last_reviewed_at: '2026-06-20'
source_type: wiki
source_ref: wiki:c77c6bdf-23d4-4c31-b325-128a8f8a6d3e
tags:
- KYC
- Reminder
- EID
subdomain: eid-kyc
module: active-account
sensitivity: normal
name: KYC状态提醒接口 (check-reminder)
aliases:
- KYC Reminder
related_services:
- svc_kyc
---

## 用途
检查 KYC 状态：当用户已完成 KYC 流程并处于待确认状态时，提醒用户尽快确认 EID 信息。

## 路径/方法
- API: `/kyc/active-account/v1/kyc/check-reminder`
- Method: POST

## 入参
| 参数 | 类型 | 必填 | 示例 | 说明 |
|---|---|---|---|---|
| scene | String | Y | BOTIM_MONEY | Definition source（场景标识） |

## 出参
| 参数 | 类型 | 必填 | 示例 | 说明 |
|---|---|---|---|---|
| reminderType | String | Y | KYC_CONFIRM | Reminder type，如 KYC_CONFIRM |
| reminderMsg | String | Y | xxxxxx | description content（提醒文案） |
| icon | String | N | https://xxxxx | The picture of the page |
| link | String | N | https://xxxxx | Click on the link that redirects |
| token | String | N | 75762b77ed11445abd6078f739b53be7 | KYC flow id |

## 错误码
原文未列出该接口专属错误码。

## 测试校验点
- 入参 `scene` 必填，传入合法场景值（如 BOTIM_MONEY）能正常返回提醒数据。
- 当用户已完成 KYC 流程且处于待确认状态时，`reminderType` 应返回 `KYC_CONFIRM`。
- `reminderMsg` 必返回提醒文案；`icon`、`link`、`token` 为可选字段。
- 返回的 `token` 可作为后续 KYC flow id（用于 inquire-info / get-result 等接口）使用。
- 用户未到达"等待确认 EID 信息"状态时，应根据业务约定返回相应结果（不构造未在文档中说明的行为）。
