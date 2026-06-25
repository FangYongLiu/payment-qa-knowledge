---
id: api_kyc_passport_get_result
object_type: API
domain: kyc
status: active
owner: xinwei.cao
reviewer: xinwei.cao
last_reviewed_at: '2026-06-20'
source_type: wiki
source_ref: wiki:e75788c0-8dcd-4b0c-95e3-8c08067ad9e7
tags:
- passport
- kyc
- result
subdomain: passport
module: null
sensitivity: normal
name: 获取Passport KYC结果接口
aliases: []
related_services:
- svc_kyc
related_tables:
- tbl_kyc_tm_kyc_apply
- tbl_kyc_tr_biz_record_customer_detail
related_scenarios: []
---

## 用途
当用户完成 KYC journey 后，跳转到结果页时调用，用于展示 KYC journey 的结果（含 liveness 失败、审核中、需确认 passport 信息、成功、失败、护照过期等场景）。

## 关联关系
- **所属服务**:[[svc_kyc]](related_services;api→service 边)
- **读写的表**:待补
- **被哪些场景测**:§9 登录/KYC 回归(待补具体 scenario 对象)

## 路径/方法
- API: `/kyc/active-account/v1/passport/main/get-result`
- Method: POST
- Domain:
  - SIM: `https://sim.test2pay.com/cgs/api`
  - UAT/PROD: 同前缀域名

## 入参
Request body：

| Parameter | Data Type | Mandatory | Example | Description |
|---|---|---|---|---|
| token | String | Y | 75762b77ed11445abd6078f739b53be7 | flow id |

## 出参
Response body：

| Parameter | Data Type | Mandatory | Example | Description |
|---|---|---|---|---|
| commandType | String | Y | moveForward | tips: show tips；moveForward: go to the next step；action |
| commandData | json | Y | TipsInfo or action | commandType=tips 返回 TipsInfo；commandType=moveForward 返回 next step |

commandData（action 场景，passportInfo）：

| Parameter | Data Type | Mandatory | Example | Description |
|---|---|---|---|---|
| passportInfo | EidInfo | N | - | Eid information，name 与 Eid number 需 RSA 加密 |
| --passportNumber | String | Y | 784XXXXXXXXXX | The number on Eid |
| --nameEnglish | String | Y | SanZhang | english name |
| --birthDate | String | Y | 1992-01-01 | yyyy-MM-dd |
| --nationality | String | Y | India | nationality |
| --gender | String | Y | Male | - |
| --expiryDate | String | Y | 2026-12-01 | yyyy-MM-dd |

响应示例覆盖场景：
1. liveness fail：commandType=tips，title="Kyc fail"，redirectView 含 `Retake selfie`，viewAction.retakeTooManyFlag。
2. kyc process（审核中）：commandType=tips，title="We are verifying your account"，redirectView 含 `Okay`。
3. confirm：commandType=action，commandData.passportInfo（nameEnglish、passportNumber 等）。
4. kyc success：commandType=tips，title="Kyc success"，含 tipContent。
5. kyc fail：commandType=tips，title="We couldn't verify your account"。
6. ocr passport has expired：commandType=tips，title="Your Passport has expired"，redirectView 含 `Try again`。

## 错误码
- status=200 表示成功（参考 1.2 约定）；其余错误码原文未列出。

## 测试校验点
- token 必填，使用 start-journey 返回的 token。
- 校验 commandType 取值：tips / moveForward / action 三类分支处理正确。
- liveness fail 场景：返回 redirectView 中含 Retake selfie 视图，并触发 [[api_kyc_passport_retake_selfie]] 流程；retakeTooManyFlag=Y 时限制再次自拍。
- confirm 场景：commandType=action，passportInfo 字段完整（passportNumber、nameEnglish、birthDate、nationality、gender、expiryDate）；nameEnglish 与 passportNumber 需 RSA 加密验证；后续触发 [[api_kyc_passport_confirm_info]]。
- ocr passport has expired 场景：redirectView 触发重新验证 [[api_kyc_passport_verify_again]]。
- kyc process / success / fail 三类 tips 文案、tipImg、tipContent 字段展示正确。
- 用户未完成 journey 时调用应符合 start-journey 的约定（参见 [[api_kyc_passport_start_journey]]）。
