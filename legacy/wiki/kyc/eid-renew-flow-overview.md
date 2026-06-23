---
title: EID续期(EID Renew)端到端流程总览
domain: kyc
kind: wiki_page
slug: eid-renew-flow-overview
status: archived
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:PMDPayment/1201700977
tags: []
---

# EID续期(EID Renew)端到端流程总览

本页概述用户进行 EID 续期（Renew）从启动 journey 到最终成功/失败的端到端流程，覆盖正常路径与各异常分支。所有请求与响应均为 JSON 协议。

## 流程总览

EID Renew 主链路按以下顺序流转：

1. 查询 KYC 信息（参考 Eid kyc cgs api v2）
2. 启动 Renew Journey → 拉起 Signzy 采集页或回到结果页/重提交页
3. Signzy 采集完成后，查询 Renew 结果
4. 根据结果分支：确认 EID 信息 / 编辑后提交 / 重拍自拍 / 放弃 KYC / 重新验证
5. 终态：直接成功、进入人工审核、或失败

## 关键步骤与接口

- 启动 journey：[[api_kyc_eid_renew_start_journey]]，根据返回 `commandData.nextStep` 决定跳 Signzy 链接、`route://native/kyc/result` 或 `route://native/kyc/re-submit`。
- 查询结果：[[api_kyc_eid_renew_get_result]]，使用启动时返回的 `token` 作为 flow id。
- 行业选择：参考 Eid kyc cgs api v2 的 Inquire industry。
- 确认 EID 信息（不修改，不进人工审核）：[[api_kyc_eid_renew_confirm_info]]。
- 提交修改后的 EID 信息（修改即进入人工审核；未修改则无需人工审核）：[[api_kyc_eid_renew_submit_edit]]。
- 重拍自拍（liveness 失败）：[[api_kyc_eid_renew_retake_selfie]]。
- 放弃 KYC：[[api_kyc_eid_renew_leave_submit]]，记录放弃原因，不允许重新提交。
- 重新验证（OCR 信息错误时）：[[api_kyc_eid_renew_verify_again]]，开启新的 journey。

## 通用响应协议

所有上述接口共用同一种响应外壳：

- `commandType`：
  - `tips`：展示提示页/弹窗，`commandData` 为 TipsInfo
  - `moveForward`：进入下一步，`commandData` 携带 `nextStep` 与 `data.token`
  - `action`：返回业务数据（如 `eidInfo`、`completedTimes`），由前端渲染
- TipsInfo 常见字段：`type`(Page/Popup)、`title`、`tipText`、`tipImg`、`redirectView[]`(`viewName`/`viewType`/`viewUrl`/`viewImg`/`viewAction`)。

## 主要分支

### 启动 journey 分支
- 首次/继续：`nextStep` 为 Signzy 链接（如 `https://kyc-preproduction.signzy.app/...`）。
- 已完成采集：`nextStep = route://native/kyc/result`，进入结果页。
- 需要重提交：`nextStep = route://native/kyc/re-submit`。

### Get Result 分支
- liveness fail：`tips`，标题 `Kyc fail`，提供 `Retake selfie` 入口；`viewAction.retakeTooManyFlag=Y` 表示重拍次数超限。
- renew process：`tips`，提示账户审核中（最长 48 小时）。
- renew confirm：`action`，返回 `eidInfo`（含 `idNumber`/`nameEnglish`/`birthDate`/`expiryDate`/`nationality`/`gender` 等，姓名与 EID 号需 RSA 加密）与 `completedTimes`，并据 `manualEditFlag` 决定是否允许编辑。
- 跳转重提交页：`moveForward`，`nextStep = route://native/kyc/re-submit`。
- renew success / renew fail：`tips` 终态页。
- OCR EID 已过期：`tips`，提供 `Verify with UAE PASS` 与 `Try again` 两个入口。

### 确认 / 提交 EID 信息分支
- Confirm（不可修改）：成功则 `moveForward`(Popup) Kyc success；处理中显示 `Kyc complete`；失败显示 `Kyc fail`。
- Submit-edit（已修改 → 人工审核）：失败页提供 `Try again` / `Contact us`；处理中提供 `Okay`；成功为 `moveForward` Popup。

### 重拍自拍分支
- 调用 retake-selfie 后，`moveForward` 至新的 Signzy journey 链接，`data.token` 沿用原 flow id。

### 放弃 KYC 分支
- 调用 leave-submit 提交 `reason`（如 `I'm not comfortable sharing my ID`）。
- 前端无需校验响应；提交后不可再次提交。

### Verify Again 分支
- OCR 信息错误时调用，`moveForward` 至 `/kyc/home`，开启新的 Signzy renew journey。

## 数据与安全要点

- `token` 贯穿整个 Renew 流程，作为 flow id 在各接口间传递。
- `eidInfo` 中的姓名（name/nameEnglish）与 `idNumber` 在传输时需使用 RSA 加密（密文）。
- 日期字段统一格式 `yyyy-MM-dd`（`birthDate`、`expiryDate`）。
- `manualEditFlag=Y` 时允许用户编辑 EID 信息，编辑后通过 submit-edit 进入人工审核。
