---
id: api_kyc_eid_get_retake_selfie_result
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
- retake
- selfie
- liveness
subdomain: eid
module: main
sensitivity: normal
name: 获取重拍结果接口 (get-retake-selfie-result)
aliases:
- get-retake-selfie-result
related_services:
- svc_kyc
related_tables:
- tbl_kyc_tr_biz_record_live
related_scenarios: []
---

## 用途
当用户在活体认证失败后选择重新自拍 (retake-selfie) 并完成 KYC journey，调用本接口获取重拍后的 KYC 结果，前端据此跳转到结果页或后续流程。

## 关联关系
- **所属服务**:[[svc_kyc]](related_services;api→service 边)
- **读写的表**:待补
- **被哪些场景测**:§9 登录/KYC 回归(待补具体 scenario 对象)

## 路径/方法
- API: `/kyc/active-account/v1/eid/main/get-retake-selfie-result`
- Method: `POST`

## 入参
Request body：

| 参数 | 类型 | 必填 | 示例 | 说明 |
|---|---|---|---|---|
| token | String | Y | 75762b77ed11445abd6078f739b53be7 | flow id |

## 出参
Response body：

| 参数 | 类型 | 必填 | 示例 | 说明 |
|---|---|---|---|---|
| commandType | String | Y | moveForward | tips: show tips；moveForward: go to the next step；action |
| commandData | json | Y | TipsInfo or action | 1. commandType = tips, return TipsInfo；2. commandType = moveForward, get next step |

commandData (当为 action 时)：

| 参数 | 类型 | 必填 | 示例 | 说明 |
|---|---|---|---|---|
| eidInfo | EidInfo | N | | Eid information, need to encrypt(RSA) your name and Eid number |
| --cardNo | String | N | 136133886 | |
| --idNumber | String | Y | 784XXXXXXXXXX | The number on Eid |
| --nameEnglish | String | Y | SanZhang | english name |
| --birthDate | String | Y | 1992-01-01 | yyyy-MM-dd |
| --nationality | String | Y | India | nationality |
| --gender | String | Y | Male | |
| --occupation | String | N | Portnr | occupation |
| --employer | String | N | AlRiqah Spocialzed Dontal Centere | employer |
| --expiryDate | String | Y | 2026-12-01 | format: yyyy-MM-dd |

注意 (与 get-result 的差异)：response action 中包含 `manualEditFlag` 字段（示例值 `N`），不再返回 `completedTimes`。

响应示例分支：
1. **liveness fail**：`commandType=tips`，`title="Kyc fail"`，`redirectView` 提供 `Retake selfie`，其 `viewAction.retakeTooManyFlag="N"`（区别于 get-result 中可能为 `Y`）。
2. **kyc process**：`commandType=tips`，`title="We are verifying your account"`，提示最长 48 小时审核。
3. **confirm**：`commandType=action`，`commandData` 含 `manualEditFlag:"N"` 与 `eidInfo`(name/idNumber 等)。
4. **go to the reSubmit eid page**：`commandType=moveForward`，`nextStep="route://native/kyc/re-submit"`，`data.token` 返回 flow id。
5. **kyc success**：`commandType=tips`，`title="Kyc success"`。
6. **kyc fail**：`commandType=tips`，`title="We couldn't verify your account"`。

## 错误码
原文未单独列出错误码；以 `status=200` 表示成功（沿用同模块约定）。

## 测试校验点
- token 必填，需为 retake-selfie 启动后的同一 flow id。
- 校验 6 类响应分支均能正确渲染：liveness fail / kyc process / confirm / re-submit / kyc success / kyc fail。
- liveness fail 分支中 `retakeTooManyFlag="N"`，需校验前端在该值下仍允许再次重拍（与 get-result 中 `Y` 的禁用态区分）。
- confirm 分支返回 `manualEditFlag`（本接口为 `N`，区别于 get-result 的 `manualEditFlag=Y`），校验前端是否按此控制 EID 信息是否可手工编辑。
- `eidInfo` 中 `name` 与 `idNumber` 需为 RSA 加密后的密文。
- re-submit 分支 `nextStep="route://native/kyc/re-submit"` 时，`data.token` 必须回传。
- kyc process 分支 `redirectView` 的 "Okay" 按钮跳转 `viewUrl` 是否生效。
- 必填字段缺失/异常 token 时的接口行为。
