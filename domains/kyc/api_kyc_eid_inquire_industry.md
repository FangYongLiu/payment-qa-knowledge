---
id: api_kyc_eid_inquire_industry
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
- industry
subdomain: eid
module: active-account
sensitivity: normal
name: 查询行业列表接口 (inquire-industry)
aliases:
- inquire-industry
related_services:
- svc_kyc
---

## 用途
获取行业列表，供用户在确认 EID 信息（confirm-info）或提交修改 EID 信息（submit-edit）时选择一个行业项作为 `industry` 入参。

## 路径/方法
- 路径：`/kyc/active-account/v1/eid/inquire-industry`
- Method：POST

## 入参
Request body 无业务字段（文档中未列出业务参数）。

## 出参
| 参数 | 类型 | 必填 | 示例 | 描述 |
|---|---|---|---|---|
| industryList | List<Item> | Y | - | 行业列表 |
| --value | String | Y | High Value Goods Dealers | 行业信息的 value，提交时使用此值 |
| --name | String | Y | High Value Goods Dealers | 行业信息的 key |

## 错误码
原文未提供该接口的专属错误码。

## 测试校验点
- 请求 `/kyc/active-account/v1/eid/inquire-industry` POST 成功后返回 `industryList`，每项包含 `value` 和 `name` 两个非空字段。
- 返回的 `value` 可作为后续 `confirm-info` 与 `submit-edit` 接口中 `industry` 字段的入参（如 `High Value Goods Dealers`）。
- 校验提交场景：用户选择列表中某项 `value` 后，confirm-info / submit-edit 能被成功接受。
- 列表为空或字段缺失（value/name 任一为空）属于异常。
