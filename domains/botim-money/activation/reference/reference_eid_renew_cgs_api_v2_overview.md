---
id: reference_eid_renew_cgs_api_v2_overview
object_type: Reference
name: EID Renew CGS API v2 总览
aliases: [eid-renew-cgs-api-v2-overview]
domain: activation
status: active
owner: xinwei.cao
reviewer: xinwei.cao
source_type: wiki
source_ref: wiki:af2b7970-1661-4d20-90f7-3b86b8f72d58
tags: [activation, wiki-overview]
related_services: [svc_kyc]
related_tables: [tbl_kyc_tm_audit_task, tbl_kyc_tm_biz_record, tbl_kyc_tm_kyc_apply, tbl_kyc_tr_biz_record_live, tbl_kyc_tr_biz_record_ocr]
---


# EID Renew CGS API v2 总览

本页概述 EID 续期（Renew）流程的端到端调用顺序、各接口职责，以及统一的 `commandType` / `commandData` 交互模型（业务域 domain=kyc）。

## 环境域名

- SIM: `https://sim.test2pay.com/cgs/api`
- UAT: （待补充）
- PROD: （待补充）
- 所有 request/response body 均使用 JSON 协议。

## 端到端调用顺序

EID Renew 流程涉及以下步骤（按章节顺序）：

1. Inquire kyc information（参见 Eid kyc cgs api v2）
2. Start Eid renew journey — [[api_kyc_eid_renew_start_journey]]
3. Get result — [[api_kyc_eid_renew_get_result]]
4. Inquire industry（参见 Eid kyc cgs api v2）
5. Confirm Eid information — [[api_kyc_eid_renew_confirm_info]]
6. Submit Eid information — [[api_kyc_eid_renew_submit_edit]]
7. Retake selfie — [[api_kyc_eid_renew_retake_selfie]]
8. Leave kyc — [[api_kyc_eid_renew_leave_submit]]
9. Verify again — [[api_kyc_eid_renew_verify_again]]

## 各接口职责

| 步骤 | API 路径 | 职责 |
|---|---|---|
| Start journey | `/kyc/active-account/v1/eid/renew/start-journey` | 启动续期流程，创建 journey url；若已执行过则直接返回结果 |
| Get result | `/kyc/active-account/v1/eid/renew/get-result` | 用户完成 journey 后查询结果，进入结果页或确认/重交页 |
| Confirm info | `/kyc/active-account/v1/eid/renew/confirm-info` | 用户确认 EID 信息（不修改）；不进入人工审核 |
| Submit edit | `/kyc/active-account/v1/eid/renew/submit-edit` | 用户确认修改后的 EID 信息；有修改则进入人工审核，无修改则跳过 |
| Retake selfie | `/kyc/active-account/v1/eid/renew/retake-selfie` | liveness 失败后用户选择重拍自拍 |
| Leave submit | `/kyc/active-account/v1/eid/renew/leave-submit` | 记录用户放弃 KYC 的原因，不可重交；前端无需校验响应 |
| Verify again | `/kyc/active-account/v1/eid/renew/verify-again` | 当 EID OCR 信息有误时，重新发起一次新的 journey |

## commandType / commandData 交互模型

所有响应使用统一的 `commandType` + `commandData` 结构来驱动客户端行为。

### commandType 取值

- `tips`：展示提示页/弹窗，`commandData` 返回 `TipsInfo`
- `moveForward`：进入下一步，`commandData` 返回 action（含 `nextStep` 与 `data`）
- `action`：返回业务数据（如 `eidInfo`、`completedTimes` 等）供页面渲染

### moveForward 常见 nextStep

- 外链 signzy journey：如 `https://kyc-preproduction.signzy.app/pUwEHit`
- 结果页：`route://native/kyc/result`
- 重交 EID 页：`route://native/kyc/re-submit`
- 首页：`/kyc/home`
- 附带 `data.token`（flow id）用于后续接口调用

### TipsInfo（tips 场景）

- `type`：`Page` 或 `Popup`
- `title` / `tipText` / `tipImg`
- `redirectView[]`：可选的跳转按钮列表，含 `viewName` / `viewType` / `viewUrl` / `viewImg` / `viewAction`

### 典型 tips 业务场景

- liveness fail（含 `retakeTooManyFlag` 标识）
- renew process（审核中，最多 48 小时）
- renew success / renew fail
- ocr eid has expired（提示使用 UAE PASS 或 Try again）

## 关键字段约定

- `token`：flow id，贯穿 Get result / Confirm / Submit edit / Retake selfie / Leave / Verify again 各接口
- `eidInfo`：EID 信息对象，其中 `name` 与 `idNumber` 需 RSA 加密传输
- 日期字段（`birthDate` / `expiryDate`）格式：`yyyy-MM-dd`
- HTTP `status=200` 表示成功

## 人工审核分支

- Confirm info：用户未修改信息，不进入人工审核
- Submit edit：用户修改了 EID 信息后进入人工审核；未修改则无需审核
