---
id: tbl_merchant_db
object_type: Table
domain: merchant-management
status: active
owner: yijian.tan
reviewer: yijian.tan
last_reviewed_at: '2026-06-18'
source_type: wiki
source_ref: confluence:tester/124289264
tags:
- 商户
- 门店
- 员工
- 账期
- 定时出款
subdomain: merchant
module: null
sensitivity: normal
name: 商户库(merchant)核心表
aliases:
- merchant
related_services:
- svc_merchant
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

## 用途
merchant 库存放商户域核心数据，覆盖商户、门店、员工及角色、账期与定时出款等业务对象，是商户身份、组织结构、出款策略相关查询的入口。

## 关键列
- `t_merchant`：商户表
  - `mid`：商户号
  - `id`：商户 id
- `t_store`：门店表
  - `merchant_id`：商户 id
  - `id`：门店 id
- `t_staff`：员工表(门店下员工)
- `t_staff_role`：员工角色表
- `t_period`：账期表
- `t_auto_withdraw_registration`：定时出款设置表
- `t_auto_withdraw_order`：定时出款订单表

## 主键/索引
原文未提供，按表内 `id` / `mid` / `merchant_id` 等字段作为业务主键与关联键使用。

## 校验点(QA 关注)
- 商户层级关系：`t_merchant.id` → `t_store.merchant_id` → `t_staff` 关联是否完整。
- 商户号 `mid` 与商户 id `id` 不要混用：对外业务通常用 `mid`，库内关联用 `id`。
- 员工与角色：`t_staff` 与 `t_staff_role` 的角色挂载是否正确，影响权限。
- 账期 `t_period` 与定时出款：`t_auto_withdraw_registration` 配置是否生效，对应是否生成 `t_auto_withdraw_order` 出款订单。
- 与设备库 [[tbl_device_db]] 的 `t_merchant_device` 关联，确认商户-设备绑定一致；与费率 [[tbl_ppcenter_db]]、[[tbl_pbsdb_db]]、账单 [[tbl_statementii_db]] 联动验证。
