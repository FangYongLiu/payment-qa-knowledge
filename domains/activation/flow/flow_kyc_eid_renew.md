---
id: flow_kyc_eid_renew
object_type: Flow
name: EID 续期端到端流程 (EID Renew)
aliases: [EID续期流程, eid-renew-flow]
domain: activation
status: active
owner: xinwei.cao
reviewer: xinwei.cao
last_reviewed_at: '2026-06-25'
source_type: wiki
source_ref: legacy/wiki/kyc/eid-renew-flow-overview.md + eid-renew-cgs-api-v2-overview.md(整合)
tags: [kyc, eid, renew, 续期, 流程]
related_services: [svc_kyc]
related_tables: [tbl_kyc_tm_kyc_apply, tbl_kyc_tr_biz_record_ocr, tbl_kyc_tr_biz_record_ica, tbl_kyc_tm_eid_expiry_notify_event]
related_scenarios: []
---

# EID 续期端到端流程 (EID Renew)

> EID 过期后用户重新走 journey 完成续期。统一 `commandType`/`commandData` 交互模型;JSON 协议;挂 `cgs/api` 域。

## 概述
EID Renew 主链路:**查询 KYC 信息 → 启动 Renew Journey(拉起 Signzy 采集页 / 回结果页 / 重提交页)→ Signzy 采集完成 → 查询 Renew 结果 → 分支(确认 / 编辑后提交 / 重拍自拍 / 放弃 / 重新验证)→ 终态(直接成功 / 进人工审核 / 失败)**。

## 步骤(跨系统)与接口
1. 查 KYC 信息(`inquire-info`)。
2. 启动 journey:[[api_kyc_eid_renew_start_journey]] —— `commandData.nextStep` 决定跳 Signzy 链接 / `route://native/kyc/result` / `route://native/kyc/re-submit`。
3. 查结果:[[api_kyc_eid_renew_get_result]](用启动返回的 `token` 作 flow id)。
4. 分支处理:
   - 确认 EID 信息(不改、免人审):[[api_kyc_eid_renew_confirm_info]]
   - 提交修改(改即进人审,未改免审):[[api_kyc_eid_renew_submit_edit]]
   - 重拍自拍(liveness 失败):[[api_kyc_eid_renew_retake_selfie]]
   - 放弃(记录原因,不可重提):[[api_kyc_eid_renew_leave_submit]]
   - 重新验证(OCR 错):[[api_kyc_eid_renew_verify_again]](开新 journey)

## 通用响应协议(commandType / commandData)
- `tips`:展示提示页/弹窗,`commandData=TipsInfo`(`type` Page/Popup、`title`、`tipText`、`tipImg`、`redirectView[]`)。
- `moveForward`:进入下一步,携 `nextStep` + `data.token`。
- `action`:返回业务数据(如 `eidInfo`、`completedTimes`),前端渲染。

## 主要分支
- **启动 journey**:首次/继续→Signzy 链接;已采集→`route://native/kyc/result`;需重提交→`route://native/kyc/re-submit`。
- **Get Result**:liveness fail→`tips` 标题 `Kyc fail` + `Retake selfie` 入口(`viewAction.retakeTooManyFlag=Y` 表重拍超限)。

## 关联关系
- **经过的服务**:[[svc_kyc]](+ Signzy 外部采集)
- **读写的表**:[[tbl_kyc_tm_kyc_apply]]、[[tbl_kyc_tr_biz_record_ocr]]、[[tbl_kyc_tr_biz_record_ica]];过期驱动见 [[tbl_kyc_tm_eid_expiry_notify_event]]

## 校验点
- `token` 贯穿续期全程;`completedTimes`/重拍超限标记。
- 续期"改信息→人审、不改→免审"分支正确。
- 终态成功 → `tm_kyc_apply.success_time` 写;过期判断与 `tm_eid_expiry_notify_event` 一致。
