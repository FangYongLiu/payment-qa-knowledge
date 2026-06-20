---
title: KYC Change Mobile 换绑手机号流程
domain: kyc
kind: wiki_page
slug: kyc-change-mobile-flow
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki
source_ref: wiki:2654d3b2-24d5-481b-926b-96f41f946ae8
tags: []
---

# KYC Change Mobile 换绑手机号流程

本页描述 EID KYC 在换绑手机号场景下，前端通过 CGS `confirm-change-mobile` 接口与后端 Member Dubbo 接口协同完成账号释放与换绑刷新 KYC 的流程，以及不同结果的展示规则。

## 流程概览

1. 前端调用 [[api_kyc_confirm_change_mobile]]（`/kyc/active-account/v1/eid/main/confirm-change-mobile`），传入 `token` 与 `id`。
2. 后端通过 [[api_member_query_eid_bound_account]] 根据 `eidNum` 查询 EID 已绑定的会员账号列表，供用户选择需要换绑的钱包。
3. 用户确认后，后端调用 [[api_member_change_mobile_refresh_kyc]]，对 `originalMemberId` 与 `newMemberId` 执行释放并换绑手机号、刷新 KYC（`scene=changeMobile`）。
4. CGS 接口根据处理结果返回不同的 `commandType` 与 `commandData`，前端按页面/弹窗展示。

## CGS 返回结构

- `commandType`：
  - `tips`：展示提示信息（`commandData` 为 `TipsInfo`）
  - `moveForward`：进入下一步（`commandData` 为下一步指令）
  - `action`：需要响应业务事项
- `commandData` 关键字段：`tipImg`、`tipText`、`title`、`type`（`Page` / `Dialog`）、`pageCode`、`redirectView`（含 `viewName`、`viewAction.actionCode`、`viewType`、`viewUrl`）。

## 各类结果展示规则

### 1. Change Mobile Success
- `type=Page`，`pageCode=kycSuccess`
- 标题：`You're all set!`
- 文案：`Your account is now active.`
- 图片：`new_success.png`

### 2. Change Mobile Pending
- `type=Page`，`pageCode=kycPending`
- 标题：`We are verifying your account`
- 文案：`It may take up to 48 hours to verify your account. We'll notify you as soon as it's ready.`
- 图片：`new_pending.png`
- 按钮：`Okay`（`primary`，`actionCode=close_mini_program`）

### 3. Change Mobile Failed
- `type=Page`，`pageCode=kycFail`
- 标题：`We couldn't verify your account`
- 文案：`You can try again or contact our support team for help.`
- 图片：`new_failed.png`
- 按钮：
  - `Try again`（`primary`，跳转 `/kyc/home`）
  - `Contact us`（`default`，跳转 `https://botim.me/oa/chat?oaid=IDVTFY5`）

### 4. Change Mobile Exception
- `type=Dialog`，`pageCode=chgMobExp`
- 标题：`Account connection failed`
- 文案：`Your account couldn't be linked to your mobile number. Check your connection and try again.`
- 按钮：`Try again`（`primary`，跳转 `/kyc/choose-account`）

### 5. Common Verification Exception
- `type=Dialog`（无 `pageCode`）
- 文案：`Information verification failed. Please try again later.`
- 按钮：`OK`（`default`）

## 关联 Dubbo 接口

- 查询 EID 绑定账号：[[api_member_query_eid_bound_account]]，返回 `memberAccountList`（含 `mobileMask`、`mobileTicket`、`memberId`、`isLock`、`balance`）。
- 释放并换绑刷新 KYC：[[api_member_change_mobile_refresh_kyc]]，使用 `originalMemberId`（要换绑的钱包）、`newMemberId`（要释放的钱包）及新 `KycInfo`，`scene` 固定为 `changeMobile`。
