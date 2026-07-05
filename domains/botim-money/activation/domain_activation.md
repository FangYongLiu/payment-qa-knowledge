---
id: domain_activation
object_type: Domain
name: activation
aliases: [member, 会员, 身份, identity, KYC, 实名认证, EID, Passport]
domain: activation
business_line: botim-money
status: active
owner: xinwei.cao
reviewer: xinwei.cao
dev_owner: yadong.lu
last_reviewed_at: '2026-06-26'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md + UAT Kibana trace
tags: [activation, member, 会员, KYC, 实名认证]
related_services: [svc_member, svc_member_front, svc_member_feature, svc_kyc, svc_kyc_service, svc_ppcenter, svc_pts, svc_user_profile_scheduler, svc_palm_id]
---

# activation(身份 / 会员 + KYC)

> 域入口。全系统唯一身份实体 + 实名认证。owner xinwei.cao / 研发 Activation 团队(Yadong Lu)。

## 概述
两块合一(同属 Activation 团队):
1. **会员 / 身份(member)** — 全系统唯一的用户账户/身份实体,被所有域引用;含会员核心、front/feature、支付产品中心 ppcenter、令牌核验 pts、用户档案 user-profile。
2. **KYC 实名认证** — EID(阿联酋身份证)/ Passport(护照)两类核验 journey:OCR 识别 → 活体(liveness / palm-id 掌纹)→(必要时)人工审核 → 结果回传;含续期、换绑、重验等分支。

## 本域内容
- **service/** — member/member-front/member-feature、kyc/kyc-service、ppcenter、pts、user-profile-scheduler、palm-id。
- **table/** — member、kyc、ppcenter。
- **api/**(33,KYC 为主)· **flow/**(3)· **scenario/**(5)· **troubleshooting/**(4)。

## 相邻域
监管合规(AML/Edit42/报送)→ [[domain_compliance]];风控 → [[domain_risk]];钱包账户 → [[domain_wallet]]。

## 参考 / 流程索引(补)
- [[reference_kyc_channel_overview]](KYC 渠道总览)· [[reference_passport_kyc_s_model_api_overview]](Passport KYC S-Model API)
- [[reference_eid_renew_cgs_api_v2_overview]](EID Renew CGS API v2)· [[flow_eid_renew_flow_overview]](EID 续期端到端流程)
- [[reference_botim_payby_server_integration_overview]](Botim-PayBy 服务端集成方案)
