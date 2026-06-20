---
id: api_kyc_eid_get_retake_selfie_result
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
- liveness
- retake
subdomain: eid
module: main
sensitivity: normal
name: 获取重新自拍结果接口
aliases:
- Get retake selfie result
related_services: []
related_tables: []
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
当用户完成重新自拍（retake selfie）的 KYC journey 后，调用该接口进入结果页，展示重新自拍后的活体认证/KYC 结果。根据返回的 commandType / commandData 跳转到对应页面（提示页、确认页、re-submit 页面等）。

## 路径/方法
- API: `/kyc/active-account/v1/eid/main/get-retake-selfie-result`
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
| commandData | json | Y | TipsInfo or action | 1) commandType=tips 返回 TipsInfo；2) commandType=moveForward 获取下一步 |

commandData（当 commandType=action 时）：

| Parameter | Data Type | Mandatory | Example | Description |
|---|---|---|---|---|
| eidInfo | EidInfo | N |  | Eid information，name 与 idNumber 需要 RSA 加密 |
| --cardNo | String | N | 136133886 |  |
| --idNumber | String | Y | 784XXXXXXXXXX | The number on Eid |
| --nameEnglish | String | Y | SanZhang | english name |
| --birthDate | String | Y | 1992-01-01 | yyyy-MM-dd |
| --nationality | String | Y | India | nationality |
| --gender | String | Y | Male |  |
| --occupation | String | N | Portnr | occupation |
| --employer | String | N | AlRiqah Spocialzed Dontal Centere | employer |
| --expiryDate | String | Y | 2026-12-01 | yyyy-MM-dd |

Response 示例分支：
1. liveness fail：commandType=tips，title="Kyc fail"，redirectView 含 `Retake selfie`，`viewAction.retakeTooManyFlag="N"`。
2. kyc process：commandType=tips，title="We are verifying your account"，redirectView 含 `Okay`。
3. confirm：commandType=action，commandData 含 `manualEditFlag:"N"` 与 `eidInfo`（name、idNumber 等）。
4. go to the reSubmit eid page：commandType=moveForward，nextStep=`route://native/kyc/re-submit`，data 含 token。
5. kyc success：commandType=tips，title="Kyc success"。
6. kyc fail：commandType=tips，title="We couldn't verify your account"，tipText="Kyc fail"。

## 错误码
原文未列出该接口的具体错误码（仅说明 HTTP status=200 表示成功，由通用 commandType 区分业务分支）。

## 测试校验点
- token 为必填，缺失/错误时应失败。
- 返回 commandType 仅可能为 `tips` / `moveForward` / `action`，前端需按类型分别处理。
- 当 liveness 失败时，需校验 `redirectView[].viewAction.retakeTooManyFlag` 取值（本接口示例返回 `N`，与 get-result 的 `Y` 区分），用于决定能否再次重试自拍。
- commandType=action 分支需校验 `manualEditFlag`（示例为 `N`，即不允许手动编辑），与 get-result 的 `manualEditFlag=Y` 行为不同。
- eidInfo 中 name、idNumber 字段是否经 RSA 加密返回。
- 必填字段：idNumber、nameEnglish、birthDate、nationality、gender、expiryDate 完整性校验；可选：cardNo、occupation、employer。
- moveForward 跳转 `route://native/kyc/re-submit` 时 data.token 应回传当前 flow id。
- kyc success / kyc fail / kyc process 文案与 tipImg、redirectView 是否符合定义。
- 与 retake-selfie 接口（`/kyc/active-account/v1/eid/main/retake-selfie`）的 token 是否一致并构成完整流程。
