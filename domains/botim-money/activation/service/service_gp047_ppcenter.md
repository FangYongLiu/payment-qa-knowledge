---
id: svc_ppcenter
object_type: Service
domain: activation
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp047
name: ppcenter
dev_owner: Yadong.Lu
aliases: [gp047_ppcenter]
related_services: [svc_member, svc_acs, svc_contract]
related_tables:
- tbl_ppcenter_t_advance_define
- tbl_ppcenter_t_advance_value
- tbl_ppcenter_t_biz_product
- tbl_ppcenter_t_biz_product_group
- tbl_ppcenter_t_biz_product_mapping
- tbl_ppcenter_t_biz_product_tag
- tbl_ppcenter_t_calculation_apply
- tbl_ppcenter_t_calculation_attr
- tbl_ppcenter_t_calculation_define
- tbl_ppcenter_t_calculation_value
- tbl_ppcenter_t_clearing_apply
- tbl_ppcenter_t_clearing_attr
- tbl_ppcenter_t_clearing_define
- tbl_ppcenter_t_clearing_value
- tbl_ppcenter_t_config_audit_log
- tbl_ppcenter_t_config_data_log
- tbl_ppcenter_t_data_apply
- tbl_ppcenter_t_gateway_define
- tbl_ppcenter_t_gateway_value
- tbl_ppcenter_t_merchant_config_apply
- tbl_ppcenter_t_merchant_config_relation
- tbl_ppcenter_t_merchant_product_order
- tbl_ppcenter_t_package_template
- tbl_ppcenter_t_package_template_relation
- tbl_ppcenter_t_pay_auth_define
- tbl_ppcenter_t_pay_auth_value
- tbl_ppcenter_t_price_cal
- tbl_ppcenter_t_product_apply_info
- tbl_ppcenter_t_product_apply_order
- tbl_ppcenter_t_product_apply_relation
- tbl_ppcenter_t_product_audit_log
- tbl_ppcenter_t_product_package
- tbl_ppcenter_t_product_package_relation
- tbl_ppcenter_t_product_push_redo
- tbl_ppcenter_t_sec_merchant_cal_info
- tbl_ppcenter_t_statement_define
- tbl_ppcenter_t_statement_value
---

# ppcenter

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp047` · domain=`payment-core`。

## 作用
产品中心（商户开通产品状态 queryMerchantOpenedProductStatus，被 acquire/device/merchant-fundout 调用）

## 系统中的位置
- 功能层:营销 / 产品 / 报价 (Marketing / Product / Quote)
- 业务域:`payment-core`

## 关联关系
**调用(下游)—— 本服务依赖:**
- [[svc_member]] member（会员 / 账户核心） · 1820 次 · high
- [[svc_acs]] acs（反欺诈 / 风控 + 渠道密钥） · 102 次 · high
- [[svc_contract]] contract · 14 次 · high

**被调用(上游)—— 这些服务调用本服务:**
device, acquireii, merchant-fundout

## 参与的业务场景(cgs 回归)
- §1. 直连支付 / 预授权 / DCC（toB，`test_direct_pay` / `test_pre_auth_capture` / `test_bpg_paypage`）

## 关键方法 / 入口
queryMerchantOpenedProductStatus

## 涉及的 API / 数据库表
- **暴露/相关 API**:待补
- **读写的表**:待补

## 测试要点 / 排障 / 常见问题
- 待补(QA 视角:怎么测、已知坑、典型故障与定位)。

## 相关流程 / 场景 / 排障(反向)
本服务涉及的流程/场景/排障(由对方 `related_services` 指向,反向汇总):
- [[flow_acquire_product_application]](流程:收单商户控台产品申请与开通流程)
- [[flow_cashier_payment]](流程:收银台 / 收单卡支付端到端流程（含退款）)
- [[flow_merchant_onboarding]](流程:商户注册与入驻端到端流程(Acquire + WPS))

## 来源与置信
- UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp047` · domain=`payment-core`。
