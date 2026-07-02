---
id: flow_kyc_change_mobile
object_type: Flow
name: KYC 换绑手机号端到端流程 (Change Mobile)
aliases: [换绑手机流程, kyc-change-mobile-flow]
domain: activation
status: active
owner: xinwei.cao
reviewer: xinwei.cao
last_reviewed_at: '2026-06-25'
source_type: wiki
source_ref: legacy/wiki/kyc/kyc-change-mobile-flow.md(整合)
tags: [kyc, change-mobile, 换绑手机, 流程]
related_services: [svc_kyc, svc_member]
related_tables: [tbl_kyc_tr_biz_record_change_mobile, tbl_kyc_tm_kyc_apply]
related_scenarios: []
---

# KYC 换绑手机号端到端流程 (Change Mobile)

> EID KYC 换绑手机场景:前端经 CGS `confirm-change-mobile` 与后端 Member Dubbo 接口协同完成账号释放与换绑刷新 KYC,按结果渲染不同页面。

## 概述
用户在实名态下换绑手机号,把 EID 已绑定的某钱包账号释放并把手机号换绑到新账号,同时刷新 KYC(`scene=changeMobile`)。

## 步骤(跨系统)
1. 前端调用 [[api_kyc_confirm_change_mobile]](`/kyc/active-account/v1/eid/main/confirm-change-mobile`),传 `token` + `id`。
2. 后端按 `eidNum` 查 EID 已绑定的会员账号列表(member dubbo `query-eid-bound-account`,**接口对象待补**),供用户选择要换绑的钱包。
3. 用户确认后,后端调 member dubbo `change-mobile-refresh-kyc`(**接口对象待补**),对 `originalMemberId` 与 `newMemberId` 执行释放 + 换绑手机 + 刷新 KYC(`scene=changeMobile`)。落 [[tbl_kyc_tr_biz_record_change_mobile]]。
4. CGS 按处理结果返回 `commandType`/`commandData`,前端按页面/弹窗渲染。

## CGS 返回结构
- `commandType`:`tips`(提示)/`moveForward`(下一步)/`action`(业务事项)。
- `commandData` 关键字段:`tipImg`、`tipText`、`title`、`type`(Page/Dialog)、`pageCode`、`redirectView`(`viewName`/`viewAction.actionCode`/`viewType`/`viewUrl`)。

## 各结果渲染规则
| 结果 | type/pageCode | 标题 | 文案 | 图 | 按钮 |
|---|---|---|---|---|---|
| Success | Page / kycSuccess | You're all set! | Your account is now active. | new_success.png | — |
| Pending | Page / kycPending | We are verifying your account | …up to 48 hours… | new_pending.png | Okay(close_mini_program) |
| Failed | Page / kycFail | We couldn't verify your account | You can try again or contact support. | new_failed.png | Try again(→`/kyc/home`) |

## 关联关系
- **经过的服务**:[[svc_kyc]](CGS confirm-change-mobile)→ [[svc_member]](查 EID 绑定账号 + 换绑刷新 KYC)
- **读写的表**:[[tbl_kyc_tr_biz_record_change_mobile]]、[[tbl_kyc_tm_kyc_apply]]

## 校验点
- `originalMemberId`/`newMemberId` 释放与换绑正确;手机号密文。
- 三种结果(Success/Pending/Failed)页面渲染与 pageCode 一致;Pending 48h 提示。
- 换绑后原账户处理与会员态/实名态一致性;`scene=changeMobile` 刷新 KYC。
- ⚠ member dubbo 两个接口(query-eid-bound-account / change-mobile-refresh-kyc)**尚无接口对象,待补**。
