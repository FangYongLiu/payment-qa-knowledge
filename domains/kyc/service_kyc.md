---
id: svc_kyc
object_type: Service
domain: kyc
status: active
owner: xinwei.cao
reviewer: xinwei.cao
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp078
name: kyc
dev_owner: 沈纲领
aliases: [gp078_kyc]
related_services: [svc_member, svc_outman, svc_acs, svc_pts]
related_tables: []
---

# kyc

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp078` · domain=`kyc`。

## 作用
实名认证（KYC，调 member）

## 系统中的位置
- 功能层:风控 / 合规 / KYC (Risk / Compliance / KYC)
- 业务域:`kyc`

## 关联关系
**调用(下游)—— 本服务依赖:**
- [[svc_member]] member（会员 / 账户核心） · 188462 次 · high
- [[svc_outman]] outman · 11206 次 · high
- [[svc_acs]] acs（反欺诈 / 风控 + 渠道密钥） · 5046 次 · high
- [[svc_pts]] pts · 4 次 · high

**被调用(上游)—— 这些服务调用本服务:**
merchant-frontend

## 涉及的 API / 数据库表
**暴露 / 相关 API:** [[api_kyc_eid_get_result]] 获取EID KYC结果接口 (get-result)、[[api_kyc_body_unauth_apply]] 未认证活体核身申请接口 (body-unauth apply)、[[api_kyc_passport_submit_passport_v2]] 提交护照信息接口(v2)、[[api_kyc_eid_renew_submit_edit]] 提交修改后EID信息接口、[[api_kyc_eid_verify_again]] 重新验证接口 (verify-again)、[[api_kyc_eid_submit_edit]] 提交修改EID信息接口 (submit-edit)、[[api_kyc_eid_renew_get_result]] 查询EID续期结果接口、[[api_kyc_passport_retake_selfie]] 重拍自拍接口、[[api_kyc_eid_inquire_industry]] 查询行业列表接口 (inquire-industry)、[[api_kyc_eid_leave_submit]] 放弃KYC接口、[[api_kyc_eid_confirm_info]] 确认EID信息接口 (confirm-info)、[[api_kyc_passport_submit]] 提交护照识别信息接口(v1)、[[api_kyc_eid_renew_retake_selfie]] 重拍自拍接口、[[api_kyc_check_reminder]] KYC状态提醒接口 (check-reminder)、[[api_kyc_passport_init]] 护照认证初始化接口、[[api_kyc_confirm_change_mobile]] KYC 确认换绑手机号接口 (confirm-change-mobile)、[[api_kyc_passport_submit_v2]] 提交护照信息接口(v2)、[[api_kyc_passport_get_result]] 获取Passport KYC结果接口、[[api_kyc_eid_renew_confirm_info]] 确认EID信息接口、[[api_kyc_eid_confirm_change_mobile]] EID Change Mobile 确认接口、[[api_kyc_eid_renew_leave_submit]] 放弃KYC接口、[[api_kyc_passport_verify_again]] 重新验证KYC接口、[[api_kyc_inquire_info]] 查询KYC信息接口 (inquire-info)、[[api_kyc_passport_start_journey]] 启动护照KYC旅程接口、[[api_kyc_passport_submit_ocr]] 提交护照OCR接口(signzy临时方案)、[[api_kyc_eid_renew_verify_again]] 重新验证EID接口、[[api_kyc_eid_get_retake_selfie_result]] 获取重拍结果接口 (get-retake-selfie-result)、[[api_kyc_passport_submit_passport_v1]] 提交护照识别信息接口(v1)、[[api_kyc_passport_liveness]] 护照活体认证接口、[[api_kyc_eid_start_journey]] 启动EID KYC Journey接口 (start-journey)、[[api_kyc_passport_confirm_info]] 确认Passport信息接口、[[api_kyc_eid_renew_start_journey]] 启动EID续期Journey接口、[[api_kyc_passport_leave_submit]] 放弃KYC接口

## 参与的业务场景(cgs 回归)
- §9. 登录 / KYC / 绑卡（basic_cases：`test_login` / `test_*eid*` / `test_bankcards`）
