---
id: api_kyc_eid_renew_get_result
object_type: API
domain: activation
status: active
owner: xinwei.cao
reviewer: xinwei.cao
last_reviewed_at: '2026-06-20'
source_type: wiki
source_ref: confluence:PMDPayment/1201700977
tags:
- eid-renew
- kyc
- result
subdomain: active-account
module: eid-renew
sensitivity: normal
name: 查询EID续期结果接口
aliases:
- Get result
related_services:
- svc_kyc
related_tables:
- tbl_kyc_tm_kyc_apply
- tbl_kyc_tm_biz_record
related_scenarios: []
---

## 用途
当用户完成 EID 续期 journey 后，前端调用该接口进入结果页，根据返回的 commandType / commandData 渲染不同结果场景：liveness 失败、续期处理中、续期信息确认、跳转 reSubmit eid 页、续期成功、续期失败、OCR 识别到 EID 已过期。

## 关联关系
- **所属服务**:[[svc_kyc]](related_services;api→service 边)
- **读写的表**:待补
- **被哪些场景测**:§9 登录/KYC 回归(待补具体 scenario 对象)

## 路径/方法
- 路径：`/kyc/active-account/v1/eid/renew/get-result`
- Method：POST
- Domain：
  - SIM：`https://sim.test2pay.com/cgs/api`
  - UAT / PROD：见环境配置

## 入参
Request body (JSON)：

| 参数 | 类型 | 必填 | 示例 | 说明 |
|---|---|---|---|---|
| token | String | Y | 75762b77ed11445abd6078f739b53be7 | flow id |

## 出参
Response body (JSON)：

| 参数 | 类型 | 必填 | 示例 | 说明 |
|---|---|---|---|---|
| commandType | String | Y | moveForward | tips：展示提示；moveForward：进入下一步 |
| commandData | json | Y | TipsInfo or action | commandType=tips → TipsInfo；commandType=moveForward → 下一步动作 |

当 commandType=action 时，commandData 字段：

| 参数 | 类型 | 必填 | 示例 | 说明 |
|---|---|---|---|---|
| manualEditFlag | String | Y | Y | 是否允许手动编辑 |
| eidInfo | EidInfo | N | - | EID 信息，name 与 idNumber 需 RSA 加密 |
| eidInfo.cardNo | String | N | 136133886 | - |
| eidInfo.idNumber | String | Y | 784XXXXXXXXXX | EID 号码 |
| eidInfo.nameEnglish | String | Y | SanZhang | 英文名 |
| eidInfo.birthDate | String | Y | 1992-01-01 | yyyy-MM-dd |
| eidInfo.nationality | String | Y | India | 国籍 |
| eidInfo.occupation | String | N | Portnr | 职业 |
| eidInfo.gender | String | Y | Male | 性别 |
| eidInfo.employer | String | N | AlRiqah Spocialzed Dontal Centere | 雇主 |
| eidInfo.expiryDate | String | Y | 2026-12-01 | yyyy-MM-dd |

返回的 7 种场景示例：

1. liveness fail：commandType=tips，TipsInfo.title="Kyc fail"，redirectView 含 `Retake selfie`，viewAction.retakeTooManyFlag="Y"。
2. renew process（处理中）：commandType=tips，title="We are verifying your account"，提示最多 48 小时，redirectView=`Okay`。
3. renew confirm（确认页）：commandType=action，commandData 含 `completedTimes`、`eidInfo`(name、idNumber 等)。
4. 跳转 reSubmit eid 页：commandType=moveForward，nextStep=`route://native/kyc/re-submit`，data.token。
5. renew success：commandType=tips，title="Kyc success"。
6. renew fail：commandType=tips，title="We couldn't verify your account"，tipText="Kyc fail"。
7. ocr eid has expired：commandType=tips，title="Your Emirates ID has expired"，redirectView 含 `Verify with UAE PASS`(带 viewImg uaepass-logo) 和 `Try again`。

## 错误码
原文未单列错误码；通过 commandType=tips + TipsInfo.title/tipText 表达失败语义（Kyc fail / EID expired 等）。HTTP status=200 表示请求成功（业务结果以 commandType 区分）。

## 测试校验点
- token 必填校验，非法/过期 token 应有合理错误返回。
- 7 种结果场景均能按预期返回对应 commandType 与 commandData：
  - liveness fail：含 Retake selfie 入口及 retakeTooManyFlag 标识。
  - renew process：展示 48 小时提示页与 Okay 按钮。
  - renew confirm：返回 completedTimes 与 eidInfo，name/idNumber 为 RSA 密文，manualEditFlag 与可编辑性逻辑一致。
  - re-submit：nextStep=`route://native/kyc/re-submit`，data.token 透传。
  - renew success / renew fail：title、tipText、tipImg 正确。
  - eid expired：提供 UAE PASS 与 Try again 两个入口。
- eidInfo 必填字段(idNumber、nameEnglish、birthDate、nationality、gender、expiryDate) 缺失时的处理。
- 日期字段格式 yyyy-MM-dd 校验（birthDate、expiryDate）。
- name 和 idNumber 的 RSA 加密/解密正确性。
- manualEditFlag=Y 时前端允许跳转编辑流（提交至 submit-edit），=N 时仅可走 confirm-info。
- 与 start-journey 返回的 result 路由 `route://native/kyc/result` 衔接正确。
