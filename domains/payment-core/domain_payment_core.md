---
id: domain_payment_core
object_type: Domain
name: payment-core
aliases: [支付核心]
domain: payment-core
product: payment
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-24'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: [payment-core, 支付核心]
related_services: [svc_ues_ws, svc_pbs, svc_dpm_accounting, svc_dpm_manager, svc_dpm_task, svc_member, svc_payment, svc_deposit, svc_pfs_payment, svc_outman, svc_software_management, svc_cgs, svc_sgs, svc_query, svc_query_datasync, svc_counter, svc_mns_listener, svc_mns_main, svc_mns_scheduler, svc_pbs_bos, svc_pcs, svc_reconciliation, svc_pcm, svc_ppcenter, svc_csc, svc_fido_mgmt, svc_fidoservice, svc_authorization_service, svc_porter, svc_otpmock, svc_otps, svc_cbs, svc_css, svc_ons, svc_authorization_token, svc_escrow, svc_ufs2, svc_protocol, svc_tradeii, svc_mcs, svc_vcs, svc_member_front, svc_mssii, svc_member_feature, svc_vis, svc_host, svc_upic, svc_comp_service, svc_basis_customer, svc_das, svc_npss_gateway, svc_ppc, svc_rdgs, svc_npss, svc_escrowii, svc_wechat_channel, svc_ifb_channel, svc_feebill, svc_pix, svc_commission, svc_cns, svc_tts, svc_visii]
---

# payment-core(支付核心)

> 业务域总览(入口节点)。owner xiaoyan.zhou。细节见各服务对象。

## 概述
支付核心域:交易(tradeii)、账务(dpm/ccdpm)、路由、会员(member)、收银台核心、协议、对账(reconciliation)、NPSS、host、风控接入等支付主链路与底座能力。

## 覆盖范围
共 63 个服务:ues-ws、pbs、dpm-accounting、dpm-manager、dpm-task、member、payment、deposit、pfs-payment、outman、software-management、cgs、sgs、query、query-datasync、counter、mns-listener、mns-main、mns-scheduler、pbs-bos、pcs、reconciliation、pcm、ppcenter、csc、fido-mgmt、fidoservice、authorization-service、porter、otpmock、otps、cbs、css、ons、authorization-token、escrow、ufs2、protocol、tradeii、mcs、vcs、member-front、mssii、member-feature、vis、host、upic、comp-service、basis-customer、das、npss-gateway、ppc、rdgs、npss、escrowii、wechat-channel、ifb-channel、feebill、pix、commission、cns、tts、visii。

## QA 关注点
- 待补。

## 流程 / 场景 / 排障 索引
本域 流程 / 场景 / 排障 / 自动化 对象索引:
- [[flow_add_funds_via_bank_card]](流程:银行卡充值(Add Funds via Bank Card)端到端流程)
- [[flow_botim_wallet_binding_auth]](流程:BOTIM 钱包绑定/登录/Token 刷新认证流程)
- [[flow_cko_subscription_payment]](流程:CKO 渠道订阅支付（签约 + 支付）时序流程)
- [[flow_h5_jsbridge_auth]](流程:H5 客户端 jsBridge 鉴权流程(Verifier Token + Session))
- [[flow_manual_fund_settlement]](流程:人工资金调拨端到端流程)
- [[flow_unionpay_card_activation]](流程:UnionPay 银联卡激活端到端流程)
- [[flow_unionpay_card_issuance]](流程:UnionPay 银联卡开卡端到端流程)
- [[scn_botim_vip_auto_sign_protocol]](场景:Botim VIP 会员协议自动签署)
- [[scn_cko_card_binding_subscription]](场景:CKO 订阅支付绑卡与签约（CKO121/CKO111）)
- [[scn_payment_core_manual_fund_settlement]](场景:人工资金调拨-产品码映射与资金流校验)
- [[scn_payment_core_mit_cit_mpgs]](场景:MIT/CIT MPGS 循环（tokenized）支付测试)
- [[scn_unionpay_usage]](场景:UnionPay 三入口使用场景(Money / 付款码 / 扫商户码 + 外币))
- [[ts_directpay_3ds_downgrade_token_invalid]](排障:DirectPay 3DS 降级导致 CardToken 代扣失败)
- [[ts_payby_auth_protocol_return_codes]](排障:PayBy 授权协议签约 / 转账接口返回码排错)
- [[ts_payment_db_navigation]](排障:支付链路数据库库表速查与排查导航)
