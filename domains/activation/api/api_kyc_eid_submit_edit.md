---
id: api_kyc_eid_submit_edit
object_type: API
domain: activation
status: active
owner: xinwei.cao
reviewer: xinwei.cao
last_reviewed_at: '2026-06-20'
source_type: wiki
source_ref: wiki:c77c6bdf-23d4-4c31-b325-128a8f8a6d3e
tags:
- EID
- KYC
- manual-review
subdomain: eid
module: main
sensitivity: normal
name: 提交修改EID信息接口 (submit-edit)
aliases:
- submit-edit
related_services:
- svc_kyc
related_tables:
- tbl_kyc_tm_biz_record
- tbl_kyc_tr_biz_record_ocr
related_scenarios: []
---

## 用途
用户在确认页修改了 EID 信息后提交确认。当用户对 OCR 出来的 Eid 信息进行了修改时，将进入人工审核阶段；若用户未做任何修改，则无需人工审核。

## 关联关系
- **所属服务**:[[svc_kyc]](related_services;api→service 边)
- **读写的表**:待补
- **被哪些场景测**:§9 登录/KYC 回归(待补具体 scenario 对象)

## 路径/方法
- API: `/kyc/active-account/v1/eid/main/submit-edit`
- Method: POST

## 入参
Request body:

| 参数 | 类型 | 必填 | 示例 | 说明 |
|---|---|---|---|---|
| token | String | Y | 75762b77ed11445abd6078f739b53be7 | flow id |
| idNumber | String | Y | 784XXXXXXXXXXX | EID number（Ciphertext） |
| name | String | Y | San zhan | name（Ciphertext） |
| birthDate | Date | Y | 1992-01-01 | format：yyyy-MM-dd |
| expiryDate | Date | Y | 2026-12-01 | format：yyyy-MM-dd |
| industry | String | Y | High Value Goods Dealers | The industry information selected by the user |

## 出参
Response body:

| 参数 | 类型 | 必填 | 示例 | 说明 |
|---|---|---|---|---|
| commandType | String | Y | tips | tips: show tips；moveForward: go to the next step；action |
| commandData | json | Y | TipsInfo | 1, commandType=tips 返回 TipsInfo；2, commandType=moveForward 进入下一步 |

响应示例分支：
1. kyc fail：`commandType=tips`，title="Kyc fail"，tipText="Kyc fail, please retry"，redirectView 含 "Try again" 与 "Contact us"。
2. kyc process：`commandType=tips`，title="Kyc complete"，tipText="Your will active wallet account"，redirectView 含 "Okay"。
3. kyc success：`commandType=moveForward`，type="Popup"，title="Kyc success"，tipText="Kyc success"。

## 错误码
原文未列出具体错误码（仅通过 commandType=tips 的 kyc fail 分支表示失败）。

## 测试校验点
- 用户修改了 EID 信息后调用 submit-edit，应进入人工审核阶段（kyc process 分支，title="Kyc complete"）。
- 用户未做任何修改时，无需人工审核（与 confirm-info 行为一致）。
- 必填字段校验：token、idNumber（密文）、name（密文）、birthDate、expiryDate、industry 均为必填。
- idNumber 与 name 须以密文（Ciphertext, RSA）传输。
- birthDate、expiryDate 格式为 yyyy-MM-dd。
- industry 应为 inquire-industry 返回列表中的 value。
- 失败分支返回 redirectView 含 "Try again" 和 "Contact us" 入口。
- 成功分支返回 commandType=moveForward，type=Popup。
