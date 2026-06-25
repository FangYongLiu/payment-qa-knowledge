---
id: tbl_pricing_db
object_type: Table
name: 费率配置相关表(ppcenter / pbsdb)
aliases:
- ppcenter
- pbs
- pbsdb
- 费率配置
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-25'
source_type: wiki
source_ref: confluence:tester/124289264
tags:
- 费率
- 产品模板
- 费率策略
- 定价
related_services:
- svc_ppcenter
- svc_pbs
related_scenarios: []
related_tables:
- tbl_pbsdb_leaf_alloc
- tbl_pbsdb_tb_bill
- tbl_pbsdb_tb_payment_order
- tbl_pbsdb_tb_pbs_bill
- tbl_pbsdb_tb_pbs_bill_detail
- tbl_pbsdb_tb_pbs_bill_strategy
- tbl_pbsdb_tb_pbs_bill_workorder
- tbl_pbsdb_tb_pbs_cachae_log
- tbl_pbsdb_tb_pbs_cal_vat_config
- tbl_pbsdb_tb_pbs_err_log
- tbl_pbsdb_tb_pbs_error_monitor
- tbl_pbsdb_tb_pbs_fee_assign
- tbl_pbsdb_tb_pbs_fee_assign_detail
- tbl_pbsdb_tb_pbs_fee_shared_strategy
- tbl_pbsdb_tb_pbs_machine_monitor
- tbl_pbsdb_tb_pbs_price_cal
- tbl_pbsdb_tb_pbs_price_cal_range
- tbl_pbsdb_tb_pbs_price_strategy
- tbl_pbsdb_tb_pbs_price_strategy_detail
- tbl_pbsdb_tb_pbs_price_strategy_log
- tbl_pbsdb_tb_pbs_price_strategy_param
- tbl_pbsdb_tb_pbs_price_strategy_unit
- tbl_pbsdb_tb_pbs_request_log
- tbl_pbsdb_tb_pbs_strategy_log
- tbl_pbsdb_tb_trade_info
- tbl_pbsdb_tm_bill_config
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
- tbl_statement_db
- tbl_trade_db
---

# 费率配置相关表(ppcenter / pbsdb)

## 用途
集中存放产品模板、费率定义/配置、产品申请审核、产品包关联,以及 PBS 费率策略与价格计算策略相关数据。涵盖两个库:
- `ppcenter`:产品模板与费率配置
- `pbsdb`:PBS 费率策略

> 这是定价域的**库级速查对象**(多库多表的清单),字段级明细以各表为准;尚无单表独立对象的字段标「待补」。

## 关联关系
- **所属服务**:[[svc_ppcenter]](产品模板/费率配置)、[[svc_pbs]](PBS 费率策略)(= frontmatter `related_services`)。
- **谁读写它**:费率配置在交易计费及账单核算中取数,见 [[tbl_trade_db]]、[[tbl_statement_db]]。
- **哪些场景校验它**:待补(尚无 `related_scenarios`)。
- 导航入口见 [[ts_payment_db_navigation]]。

## 关键列
### ppcenter 费率配置
| 表 | 说明 |
| --- | --- |
| `ppcenter.t_product_template` | 产品模板 |
| `ppcenter.t_calculation_define` | 费率定义 |
| `ppcenter.t_price_cal` | 费率配置 |
| `ppcenter.t_product_apply_order` | 产品申请 |
| `ppcenter.t_product_apply_info` | 申请审核资料 |
| `ppcenter.t_package_define` | 产品包 |
| `ppcenter.t_package_template_relation` | 产品包与产品模板的关联 |

### pbs 费率策略
| 表 | 说明 |
| --- | --- |
| `pbsdb.tb_pbs_price_strategy_unit` | 费率策略 |
| `pbsdb.tb_pbs_price_strategy_param` | 策略详情 |
| `pbsdb.tb_pbs_price_cal` | 价格计算策略 |

各表物理字段定义:待补(原文未提供)。

## 主键 / 索引
待补:原文未提供,以表内主键/外键为准。

## 校验点(QA 关注)
- 产品模板 `t_product_template` 与费率定义 `t_calculation_define`、费率配置 `t_price_cal` 的关联一致性。
- 产品申请 `t_product_apply_order` 与审核资料 `t_product_apply_info` 的对应完整性。
- 产品包 `t_package_define` 通过 `t_package_template_relation` 关联到产品模板的正确性。
- PBS 侧 `tb_pbs_price_strategy_unit` 与 `tb_pbs_price_strategy_param`、`tb_pbs_price_cal` 的策略-参数-计算链路一致。
- 与交易/账单链路的对接:费率配置在交易计费及账单核算中的取数准确性(参见 [[tbl_trade_db]]、[[tbl_statement_db]])。
