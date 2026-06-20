---
id: api_kyc_eid_get_result
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
- eid
- result
subdomain: eid
module: main
sensitivity: normal
name: 获取KYC旅程结果接口
aliases:
- Get result
related_services: []
related_tables: []
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
当用户完成 KYC journey 后进入结果页，调用此接口获取 KYC journey 的结果，并根据返回的 commandType / commandData 跳转到下一步（提示页 / 确认 EID 信息 / 重新提交 EID 等）。

## 路径/方法
- API: `/kyc/active-account/v1/eid/main/get-result`
- Method: POST

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
| commandData | json | Y | TipsInfo or action | 1, commandType=tips → TipsInfo；2, commandType=moveForward → 下一步 |

commandData（当为 action 时）字段：

| Parameter | Data Type | Mandatory | Example | Description |
|---|---|---|---|---|
| manualEditFlag | String | Y | Y | Can be edited manually |
| eidInfo | EidInfo | N | | Eid information, name 与 idNumber 需 RSA 加密 |
| --cardNo | String | N | 136133886 | |
| --idNumber | String | Y | 784XXXXXXXXXX | The number on Eid |
| --nameEnglish | String | Y | SanZhang | english name |
| --birthDate | String | Y | 1992-01-01 | yyyy-MM-dd |
| --nationality | String | Y | India | nationality |
| --occupation | String | N | Portnr | occupation |
| --gender | String | Y | Male | |
| --employer | String | N | AlRiqah Spocialzed Dontal Centere | employer |
| --expiryDate | String | Y | 2026-12-01 | format: yyyy-MM-dd |

返回示例（按场景）：

1. liveness fail（commandType=tips, redirectView 含 "Retake selfie"，viewAction.retakeTooManyFlag=Y）
2. kyc process（commandType=tips，title="We are verifying your account"，提示 48 小时内通知）
3. confirm（commandType=action，commandData 含 completedTimes、eidInfo{name,idNumber,...}）
4. go to the reSubmit eid page（commandType=moveForward，nextStep=`route://native/kyc/re-submit`，data.token）
5. kyc success（commandType=tips，title="Kyc success"）
6. kyc fail（commandType=tips，title="We couldn't verify your account"）
7. ocr eid has expired（commandType=tips，title="Your Emirates ID has expired"，redirectView 含 "Verify with UAE PASS" 与 "Try again"）

## 错误码
原文未列出此接口的错误码（仅说明 status=200 表示成功的语义未在本接口段中明示）。

## 测试校验点
- 入参 token 为 Y（必填），缺失/非法 token 应失败。
- commandType 仅取值 `tips` / `moveForward` / `action`，commandData 结构需与之匹配。
- liveness fail 场景 redirectView.viewAction.retakeTooManyFlag 取值（Y/N）应正确，控制是否允许 retake selfie。
- kyc process 提示语与图片字段（title、tipText、tipImg）正确返回。
- confirm 场景 eidInfo 中 name、idNumber 需 RSA 加密返回；manualEditFlag 字段存在且取值正确（Y 表示可手动编辑）。
- 重新提交 EID 场景 nextStep=`route://native/kyc/re-submit` 且 data.token 与请求 token 一致。
- kyc success / kyc fail 场景 type=Page，文案与图片正确。
- ocr eid expired 场景应包含 "Verify with UAE PASS" 与 "Try again" 两个 redirectView。
- EID 信息字段日期格式统一为 yyyy-MM-dd（birthDate、expiryDate）。
