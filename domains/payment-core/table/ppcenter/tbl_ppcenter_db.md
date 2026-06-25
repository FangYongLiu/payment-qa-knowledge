---
id: tbl_ppcenter_db
object_type: Table
name: 产品中心库 ppcenter 核心表(ppcenter)
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-25'
source_type: DB DDL
source_ref: DataGrip DDL export (ppcenter schema) 2026-06-25
tags:
- 费率
- 计费
- 库导航
related_services:
- svc_ppcenter
related_scenarios: []
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
# 产品中心库 ppcenter 核心表(ppcenter)

## 用途
ppcenter(产品中心)存放业务产品、算费/清结算定义与配置、商户产品开通、产品套餐模板、产品申请审核、鉴权/网关接口组等。 该对象是**库级速查/导航**(单库表清单),字段级明细以各表对象为准。

## 关联关系
- **所属服务**:[[svc_ppcenter]](= `related_services`)。
- **本库真实表**:见下表(= `related_tables`,共 37 张,均有独立表对象)。
- **谁读写它**:费率/计费在交易计费及账单核算中取数,见 [[tbl_trade_db]]、[[tbl_statement_db]]。
- 导航入口见 [[ts_payment_db_navigation]]。

## 本库表清单(37)
| 表对象 |
| --- |
| [[tbl_ppcenter_t_advance_define]] |
| [[tbl_ppcenter_t_advance_value]] |
| [[tbl_ppcenter_t_biz_product]] |
| [[tbl_ppcenter_t_biz_product_group]] |
| [[tbl_ppcenter_t_biz_product_mapping]] |
| [[tbl_ppcenter_t_biz_product_tag]] |
| [[tbl_ppcenter_t_calculation_apply]] |
| [[tbl_ppcenter_t_calculation_attr]] |
| [[tbl_ppcenter_t_calculation_define]] |
| [[tbl_ppcenter_t_calculation_value]] |
| [[tbl_ppcenter_t_clearing_apply]] |
| [[tbl_ppcenter_t_clearing_attr]] |
| [[tbl_ppcenter_t_clearing_define]] |
| [[tbl_ppcenter_t_clearing_value]] |
| [[tbl_ppcenter_t_config_audit_log]] |
| [[tbl_ppcenter_t_config_data_log]] |
| [[tbl_ppcenter_t_data_apply]] |
| [[tbl_ppcenter_t_gateway_define]] |
| [[tbl_ppcenter_t_gateway_value]] |
| [[tbl_ppcenter_t_merchant_config_apply]] |
| [[tbl_ppcenter_t_merchant_config_relation]] |
| [[tbl_ppcenter_t_merchant_product_order]] |
| [[tbl_ppcenter_t_package_template]] |
| [[tbl_ppcenter_t_package_template_relation]] |
| [[tbl_ppcenter_t_pay_auth_define]] |
| [[tbl_ppcenter_t_pay_auth_value]] |
| [[tbl_ppcenter_t_price_cal]] |
| [[tbl_ppcenter_t_product_apply_info]] |
| [[tbl_ppcenter_t_product_apply_order]] |
| [[tbl_ppcenter_t_product_apply_relation]] |
| [[tbl_ppcenter_t_product_audit_log]] |
| [[tbl_ppcenter_t_product_package]] |
| [[tbl_ppcenter_t_product_package_relation]] |
| [[tbl_ppcenter_t_product_push_redo]] |
| [[tbl_ppcenter_t_sec_merchant_cal_info]] |
| [[tbl_ppcenter_t_statement_define]] |
| [[tbl_ppcenter_t_statement_value]] |

## 校验点(QA 关注)
- 字段级以各表对象为准;此页仅作库内导航。
