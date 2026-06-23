---
id: api_kyc_eid_renew_get_result
object_type: API
domain: kyc
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-20'
source_type: wiki
source_ref: wiki:af2b7970-1661-4d20-90f7-3b86b8f72d58
tags:
- eid
- renew
- kyc
- result
subdomain: eid_renew
module: null
sensitivity: normal
name: 查询EID续期结果接口
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
当用户完成 EID 续期 journey 后，前端跳转到 result 页面调用此接口，根据后端返回的 commandType / commandData 决定下一步动作（展示提示页、跳转确认 EID 信息、跳转 re-submit、续期成功/失败、OCR 已过期、liveness 失败需重拍自拍等）。

## 路径/方法
- 路径：`/kyc/active-account/v1/eid/renew/get-result`
- Method：POST
- Domain：
  - SIM: https://sim.test2pay.com/cgs/api
  - UAT / PROD: 见总览
- 协议：JSON

## 入参
| 参数 | 类型 | 必填 | 示例 | 说明 |
|---|---|---|---|---|
| token | String | Y | 75762b77ed11445abd6078f739b53be7 | flow id |

## 出参
顶层：
| 参数 | 类型 | 必填 | 示例 | 说明 |
|---|---|---|---|---|
| commandType | String | Y | moveForward | tips：展示提示；moveForward：进入下一步；action：业务动作（如 renew confirm） |
| commandData | json | Y | TipsInfo 或 action | commandType=tips 返回 TipsInfo；commandType=moveForward 返回下一步信息；commandType=action 返回业务数据 |

当 commandType=action（renew confirm 场景）时 commandData 字段：
| 参数 | 类型 | 必填 | 示例 | 说明 |
|---|---|---|---|---|
| manualEditFlag | String | Y | Y | 是否允许手动编辑 |
| completedTimes | int | - | 2 | 已完成次数 |
| eidInfo | EidInfo | N | - | EID 信息，name / idNumber 需 RSA 加密 |
| eidInfo.cardNo | String | N | 136133886 | |
| eidInfo.idNumber | String | Y | 784XXXXXXXXXX | EID 上的号码 |
| eidInfo.nameEnglish | String | Y | SanZhang | 英文名 |
| eidInfo.birthDate | String | Y | 1992-01-01 | yyyy-MM-dd |
| eidInfo.nationality | String | Y | India | 国籍 |
| eidInfo.occupation | String | N | Portnr | 职业 |
| eidInfo.gender | String | Y | Male | 性别 |
| eidInfo.employer | String | N | AlRiqah Spocialzed Dontal Centere | 雇主 |
| eidInfo.expiryDate | String | Y | 2026-12-01 | yyyy-MM-dd |

七种典型响应分支：
1. **liveness fail**：commandType=tips，title="Kyc fail"，redirectView 含 "Retake selfie"，viewAction.retakeTooManyFlag=Y。
2. **renew process**：commandType=tips，title="We are verifying your account"，提示最长 48h 通知。
3. **renew confirm**：commandType=action，commandData 含 completedTimes、eidInfo。
4. **去 re-submit 页**：commandType=moveForward，nextStep=`route://native/kyc/re-submit`，data.token。
5. **renew success**：commandType=tips，title="Kyc success"。
6. **renew fail**：commandType=tips，title="We couldn't verify your account"。
7. **OCR EID 已过期**：commandType=tips，title="Your Emirates ID has expired"，redirectView 含 "Verify with UAE PASS" 与 "Try again"。

## 错误码
- HTTP status=200 表示成功；其余按平台通用错误码（原文未单独列错误码）。

## 测试校验点
- token 必填，缺失/非法 flow id 应失败。
- 验证七种 commandType / commandData 分支均能正确返回并被前端正确渲染：
  - liveness 失败时 redirectView 必须包含 Retake selfie，且 retakeTooManyFlag 字段透传。
  - renew process 文案与 48h 提示一致。
  - renew confirm 分支 eidInfo 中 name 与 idNumber 必须为 RSA 密文，manualEditFlag、completedTimes 正确。
  - moveForward → re-submit 时 nextStep=`route://native/kyc/re-submit`，data.token 与请求一致。
  - OCR 过期分支必须提供 UAE PASS 与 Try again 两个入口。
- 必填字段 idNumber、nameEnglish、birthDate、nationality、gender、expiryDate 在 eidInfo 中均存在。
- 日期格式 yyyy-MM-dd 校验（birthDate / expiryDate）。
- 与 [[api_kyc_eid_renew_start_journey]] 链路串联：start-journey 拿到 token → 完成 journey → get-result。
- 后续动作衔接：renew confirm → [[api_kyc_eid_renew_confirm_info]] / [[api_kyc_eid_renew_submit_edit]]；liveness fail → [[api_kyc_eid_renew_retake_selfie]]；OCR 过期 → [[api_kyc_eid_renew_verify_again]] 或放弃 [[api_kyc_eid_renew_leave_submit]]。
