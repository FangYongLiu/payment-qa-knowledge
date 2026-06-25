---
id: svc_merchant
object_type: Service
domain: portal-operations
status: active
owner: yijian.tan
reviewer: yijian.tan
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp044
name: merchant
aliases: [gp044_merchant]
related_services: [svc_aml, svc_authorization_service, svc_statementii]
related_scenarios: [scn_online_business_merchant_split]
related_tables:
- tbl_merchant_device
- tbl_merchant_t_2fa_bind_history
- tbl_merchant_t_agent_info
- tbl_merchant_t_announcement
- tbl_merchant_t_audit_content_param
- tbl_merchant_t_audit_history
- tbl_merchant_t_auto_withdraw_order
- tbl_merchant_t_auto_withdraw_registration
- tbl_merchant_t_beneficiary_model
- tbl_merchant_t_binding_card_apply_info
- tbl_merchant_t_biz_admin_info
- tbl_merchant_t_branch
- tbl_merchant_t_business_info
- tbl_merchant_t_cashier
- tbl_merchant_t_common_audit_history
- tbl_merchant_t_common_audit_order
- tbl_merchant_t_common_audit_order_ext
- tbl_merchant_t_common_batch
- tbl_merchant_t_common_batch_detail
- tbl_merchant_t_common_batch_detail_content_param
- tbl_merchant_t_common_dict
- tbl_merchant_t_compensation_event
- tbl_merchant_t_fee_type
- tbl_merchant_t_fix_qr_code
- tbl_merchant_t_group
- tbl_merchant_t_in_app_apply_order
- tbl_merchant_t_in_app_audit_history
- tbl_merchant_t_in_app_white_url
- tbl_merchant_t_lock
- tbl_merchant_t_mcc_code
- tbl_merchant_t_member_2fa_config
- tbl_merchant_t_member_2fa_scene
- tbl_merchant_t_member_setting
- tbl_merchant_t_merchant
- tbl_merchant_t_merchant_acquire_info
- tbl_merchant_t_merchant_address
- tbl_merchant_t_merchant_biz_open
- tbl_merchant_t_merchant_category
- tbl_merchant_t_merchant_category_info
- tbl_merchant_t_merchant_compliance
- tbl_merchant_t_merchant_compliance_audit_log
- tbl_merchant_t_merchant_creation_order
- tbl_merchant_t_merchant_dcc_config
- tbl_merchant_t_merchant_dcc_config_audit
- tbl_merchant_t_merchant_email
- tbl_merchant_t_merchant_in_app
- tbl_merchant_t_merchant_notes
- tbl_merchant_t_merchant_pay_type
- tbl_merchant_t_merchant_payment_gateway_info
- tbl_merchant_t_merchant_receipt
- tbl_merchant_t_merchant_status_history
- tbl_merchant_t_merchant_wps_info
- tbl_merchant_t_operation_log
- tbl_merchant_t_partner
- tbl_merchant_t_pay_link
- tbl_merchant_t_pay_link_audit
- tbl_merchant_t_pay_link_status
- tbl_merchant_t_pay_page
- tbl_merchant_t_pay_type
- tbl_merchant_t_paylink_item
- tbl_merchant_t_period
- tbl_merchant_t_product_disable_order
- tbl_merchant_t_product_enable_merchant_package
- tbl_merchant_t_product_item_info
- tbl_merchant_t_resource
- tbl_merchant_t_role
- tbl_merchant_t_role_merchant_biz_type
- tbl_merchant_t_role_resource
- tbl_merchant_t_secondary_merchant
- tbl_merchant_t_secondary_merchant_rate
- tbl_merchant_t_secondary_store
- tbl_merchant_t_secondary_terminal
- tbl_merchant_t_sequence_table
- tbl_merchant_t_staff
- tbl_merchant_t_staff_fix_qr
- tbl_merchant_t_staff_role
- tbl_merchant_t_store
- tbl_merchant_t_store_apply_info
- tbl_merchant_t_sub_merchant
- tbl_merchant_t_tax_info
- tbl_merchant_webhook_config
---

# merchant

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp044` · domain=`portal-operations`。

## 作用
商户主数据 / 商户管理（queryStaffPage/getStaff、ProductAudit、Aml）—— 被收单 / 收银 / 出款调用

## 系统中的位置
- 功能层:即时支付 / 账单 (NPSS / Bill / RTP)
- 业务域:`portal-operations`

## 关联关系
**调用(下游)—— 本服务依赖:**
- [[svc_aml]] aml（反洗钱） · 1233947 次 · high
- [[svc_authorization_service]] authorization-service（授权服务） · 4090 次 · med·待核实
- [[svc_statementii]] statementii（账单 / 对账单） · 45 次 · high

**被调用(上游)—— 这些服务调用本服务:**
merchant-frontend, merchant-fundout, cashierii, mssii, fundout, device

## 涉及的 API / 数据库表
**暴露 / 相关 API:** [[api_merchant_bizopen_wps]] 商户开通WPS接口、[[api_merchant_apply_add]] 商户申请新增接口
**读写的表:** [[tbl_merchant_device]] 商户设备关系表、[[tbl_merchant_webhook_config]] 商户Webhook配置表、[[tbl_merchant_db]] 商户库(merchant)核心表

## 参与的业务场景(cgs 回归)
- §1. 直连支付 / 预授权 / DCC（toB，`test_direct_pay` / `test_pre_auth_capture` / `test_bpg_paypage`）
- §2. 收银台 / 收银（`test_bpg_paypage` 收银侧、cashier 用例）
- §5. 银行/卡转账、出款（`test_transfer_to_bank` / `test_transfer_to_card`）

## 关键方法 / 入口
queryStaffPage, getStaff

## 测试要点 / 排障 / 常见问题
- 待补(QA 视角:怎么测、已知坑、典型故障与定位)。

## 相关流程 / 场景 / 排障(反向)
本服务涉及的流程/场景/排障(由对方 `related_services` 指向,反向汇总):
- [[auto_online_business_merchant_split]](自动化:商户分账自动化)
- [[flow_acquire_product_application]](流程:收单商户控台产品申请与开通流程)
- [[flow_merchant_onboarding]](流程:商户注册与入驻端到端流程(Acquire + WPS))
- [[scn_merchant_settlement_withdraw_auth]](场景:商户控台结算/提现/退款的双人授权)
- [[scn_online_business_merchant_split]](场景:商户分账 (Merchant Split))

## 来源与置信
- UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp044` · domain=`portal-operations`。
