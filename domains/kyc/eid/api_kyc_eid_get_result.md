---
id: api_kyc_eid_get_result
object_type: API
domain: kyc
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-20'
source_type: wiki
source_ref: wiki:c77c6bdf-23d4-4c31-b325-128a8f8a6d3e
tags:
- EID
- KYC
- result
subdomain: eid
module: main
sensitivity: normal
name: 获取EID KYC结果接口 (get-result)
aliases:
- get-result
related_services: []
related_tables: []
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
当用户完成 KYC journey 后，跳转到结果页时调用此接口，根据返回的 commandType / commandData 决定展示提示页(成功/失败/审核中/EID 过期)、跳转到 confirm 页面或 re-submit 页面。

## 路径/方法
- 路径：`/kyc/active-account/v1/eid/main/get-result`
- 方法：POST

## 入参
| 参数 | 类型 | 必填 | 示例 | 说明 |
|---|---|---|---|---|
| token | String | Y | 75762b77ed11445abd6078f739b53be7 | flow id |

## 出参
| 参数 | 类型 | 必填 | 示例 | 说明 |
|---|---|---|---|---|
| commandType | String | Y | moveForward | tips: 显示提示；moveForward: 进入下一步；action |
| commandData | json | Y | TipsInfo or action | 当 commandType=tips 返回 TipsInfo；当 commandType=moveForward 返回下一步信息 |

commandData (action 场景，commandType=action) 字段：
| 参数 | 类型 | 必填 | 示例 | 说明 |
|---|---|---|---|---|
| manualEditFlag | String | Y | Y | 是否允许手动编辑 |
| eidInfo | EidInfo | N | - | EID 信息，name 和 idNumber 需要 RSA 加密 |
| --cardNo | String | N | 136133886 | - |
| --idNumber | String | Y | 784XXXXXXXXXX | EID number |
| --nameEnglish | String | Y | SanZhang | 英文名 |
| --birthDate | String | Y | 1992-01-01 | yyyy-MM-dd |
| --nationality | String | Y | India | 国籍 |
| --occupation | String | N | Portnr | 职业 |
| --gender | String | Y | Male | 性别 |
| --employer | String | N | AlRiqah Spocialzed Dontal Centere | 雇主 |
| --expiryDate | String | Y | 2026-12-01 | yyyy-MM-dd |

## 错误码
原文未提供具体错误码列表（仅提及 status=200 表示成功，其他通过 commandType=tips 表达失败语义）。

典型响应分支（commandData 内容因场景而异）：
1. liveness fail：commandType=tips，redirectView 含 "Retake selfie"，viewAction.retakeTooManyFlag=Y
2. kyc process（审核中）：commandType=tips，标题 "We are verifying your account"，提示 48 小时内通知
3. confirm（进入确认页）：commandType=action，返回 completedTimes、eidInfo
4. 跳转 re-submit：commandType=moveForward，nextStep="route://native/kyc/re-submit"，data.token
5. kyc success：commandType=tips，标题 "Kyc success"
6. kyc fail：commandType=tips，标题 "We couldn't verify your account"
7. ocr eid 已过期：commandType=tips，标题 "Your Emirates ID has expired"，redirectView 提供 "Verify with UAE PASS" 与 "Try again"

## 测试校验点
- 必填 token 校验：缺失或非法 token 时的处理
- 各 commandType 分支前端正确路由：tips 显示对应 title/tipText/tipImg/redirectView；moveForward 按 nextStep 跳转（如 `route://native/kyc/re-submit`）；action 进入确认页并展示 eidInfo
- eidInfo 中 name、idNumber 为 RSA 加密密文，前端能正确解密/展示
- manualEditFlag=Y 时确认页允许编辑，=N 时不允许
- liveness 失败场景 retakeTooManyFlag=Y 时的引导（重拍达到上限）
- ocr eid 过期场景必须包含 UAE PASS 和 Try again 两个 redirectView
- kyc process 场景的提示语包含 48 小时内通知
- 进入 re-submit 分支时 data.token 与请求 token 一致
- 字段格式：birthDate / expiryDate 为 yyyy-MM-dd
