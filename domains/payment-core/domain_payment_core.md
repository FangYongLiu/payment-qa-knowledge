---
id: domain_payment_core
object_type: Domain
name: payment-core
aliases: [支付核心]
domain: payment-core
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
- **已知坑(UAT Kibana 7d 错误日志实测)**:[[ts_pfs_payment_account_query_fail]](支付保存账户查询异常,~153万次/7d,疑测试数据)、[[ts_reconciliation_settlement_processing]](重复结算明细 + SFTP 对账下载,~91万)、[[ts_outman_ufs_download_fail]](UFS 下载/OCR 失败,~13.7万,与 KYC 取图互为上下游)、[[ts_pbs_pricing_strategy_empty]](定价策略为空,~12万)、[[ts_ppc_compensation_customer_exists]](补偿事件 customer 已存在,疑幂等缺陷,~9万)。
- ⚠️ 多数量级极高,**需先区分 UAT 测试数据噪声 vs 真实缺陷**(详见各排障对象)。
