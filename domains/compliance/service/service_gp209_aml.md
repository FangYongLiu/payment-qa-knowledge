---
id: svc_aml
object_type: Service
domain: compliance
status: active
owner: dewen.li
reviewer: dewen.li
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp209
name: aml
dev_owner: Chao.Li
aliases: [gp209_aml]
related_services: [svc_grc_check_identity_provider, svc_member, svc_remittance, svc_vis, svc_deposit, svc_kyc_service]
related_tables:
- tbl_aml_leaf_alloc
- tbl_aml_t_aml_info_dd
- tbl_aml_t_anti_fraud
- tbl_aml_t_charge_back_product_config
- tbl_aml_t_chargeback_operator
- tbl_aml_t_chargeback_pool
- tbl_aml_t_compensation_event
- tbl_aml_t_country_config
- tbl_aml_t_device_base_info
- tbl_aml_t_device_expand_info
- tbl_aml_t_device_network_info
- tbl_aml_t_entry_account
- tbl_aml_t_event_3ds_result
- tbl_aml_t_event_type_mapping
- tbl_aml_t_fraud_pool
- tbl_aml_t_fraudpool_operation
- tbl_aml_t_freeze_order
- tbl_aml_t_freeze_task
- tbl_aml_t_geolite2_city_blocks_ipv4
- tbl_aml_t_geolite2_city_locations_en
- tbl_aml_t_identity_decision
- tbl_aml_t_identity_result
- tbl_aml_t_identity_rule
- tbl_aml_t_identity_rule_dimension
- tbl_aml_t_identity_rule_testrun_result
- tbl_aml_t_identity_type
- tbl_aml_t_identity_variables
- tbl_aml_t_inner_merchant
- tbl_aml_t_ip2location
- tbl_aml_t_label_rm_mapping
- tbl_aml_t_member_attachments
- tbl_aml_t_member_info
- tbl_aml_t_member_limit
- tbl_aml_t_member_limit_apply
- tbl_aml_t_member_limit_audit_log
- tbl_aml_t_member_limit_manual_apply
- tbl_aml_t_member_report
- tbl_aml_t_member_risk_rate
- tbl_aml_t_member_risk_rate_detail
- tbl_aml_t_member_risk_rate_his
- tbl_aml_t_member_risk_rate_log
- tbl_aml_t_member_unbind_mobile
- tbl_aml_t_payment_channel_dic
- tbl_aml_t_product_code_dic
- tbl_aml_t_random_charge_order
- tbl_aml_t_recover_funds_order
- tbl_aml_t_refund_order
- tbl_aml_t_risk_case
- tbl_aml_t_risk_case_log
- tbl_aml_t_risk_engine_score
- tbl_aml_t_risk_merge_score
- tbl_aml_t_risk_rate_list
- tbl_aml_t_risk_rate_point_config
- tbl_aml_t_risk_rate_rule
- tbl_aml_t_risk_rate_rule_item
- tbl_aml_t_risk_refund_mail
- tbl_aml_t_risk_server_switch
- tbl_aml_t_risk_status_score
- tbl_aml_t_riskresult_sendconf_items
- tbl_aml_t_rule_code
- tbl_aml_t_search_log
- tbl_aml_t_search_record
- tbl_aml_t_sms_record
- tbl_aml_t_status_score_testrun_result
- tbl_aml_t_system_param
- tbl_aml_t_temp_member
- tbl_aml_t_unfreeze_order
- tbl_aml_t_wps_control
- tbl_amlrisk_leaf_alloc
- tbl_amlrisk_t_batch_scan_info
- tbl_amlrisk_t_batch_scan_job
- tbl_amlrisk_t_compensation_event
- tbl_amlrisk_t_effective_label
- tbl_amlrisk_t_freeze_member
- tbl_amlrisk_t_member_risk_rate
- tbl_amlrisk_t_member_risk_rate_detail
- tbl_amlrisk_t_member_risk_rate_his
- tbl_amlrisk_t_member_status_control
- tbl_amlrisk_t_member_status_operate
- tbl_amlrisk_t_merchant_decision_log
- tbl_amlrisk_t_merchant_scan_info
- tbl_amlrisk_t_merchant_scan_result
- tbl_amlrisk_t_people_product
- tbl_amlrisk_t_personal_decision_log
- tbl_amlrisk_t_personal_ref
- tbl_amlrisk_t_personal_scan_info
- tbl_amlrisk_t_personal_scan_result
- tbl_amlrisk_t_relevance_file_generate
- tbl_amlrisk_t_risk_rate_list
- tbl_amlrisk_t_risk_rate_point_config
- tbl_amlrisk_t_risk_rate_rule
- tbl_amlrisk_t_risk_rate_rule_item
- tbl_amlrisk_t_sanction_list
- tbl_amlrisk_t_system_param
- tbl_amlrisk_t_transaction_alert
- tbl_amlrisk_t_transaction_alert_decision
- tbl_amlrisk_t_transaction_monitor
- tbl_amlrisk_t_transaction_type_mapping
---

# aml

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp209` · domain=`compliance`。

## 作用
反洗钱（AML），调 grc 身份校验

## 系统中的位置
- 功能层:风控 / 合规 / KYC (Risk / Compliance / KYC)
- 业务域:`compliance`

## 关联关系
**调用(下游)—— 本服务依赖:**
- [[svc_grc_check_identity_provider]] grc-check-identity-provider（风控合规身份校验） · 20172 次 · med·待核实
- [[svc_member]] member（会员 / 账户核心） · 1496 次 · high
- [[svc_remittance]] remittance（跨境汇款核心） · 522 次 · high
- [[svc_vis]] vis · 12 次 · high
- [[svc_deposit]] deposit（充值 / 存款服务） · 6 次 · high
- [[svc_kyc_service]] kyc-service（实名认证服务） · 4 次 · high

**被调用(上游)—— 这些服务调用本服务:**
merchant, remittance

## 涉及的 API / 数据库表
**读写的表:** [[tbl_aml_t_system_param]] AML系统参数表 t_system_param

## 参与的业务场景(cgs 回归)
- §7. 跨境汇款（toC，`test_remittance`）

## 关键方法 / 入口
- 待补(本窗口未单独抽取 Dubbo/RPC 方法级)。

## 测试要点 / 排障 / 常见问题
- 待补(QA 视角:怎么测、已知坑、典型故障与定位)。

## 相关流程 / 场景 / 排障(反向)
本服务涉及的流程/场景/排障(由对方 `related_services` 指向,反向汇总):
- [[flow_cashier_payment]](流程:收银台 / 收单卡支付端到端流程（含退款）)
- [[flow_merchant_onboarding]](流程:商户注册与入驻端到端流程(Acquire + WPS))

## 来源与置信
- UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp209` · domain=`compliance`。
