---
id: tbl_pbsdb_db
object_type: Table
name: 计费系统库 pbsdb 核心表(pbsdb)
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-25'
source_type: DB DDL
source_ref: DataGrip DDL export (pbsdb schema) 2026-06-25
tags:
- 费率
- 计费
- 库导航
related_services:
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
---
# 计费系统库 pbsdb 核心表(pbsdb)

## 用途
pbsdb(PBS 计费系统)存放账单、支付订单、定价策略与价格计算、分摊分润、计费工单、交易记录、账单协议等。 该对象是**库级速查/导航**(单库表清单),字段级明细以各表对象为准。

## 关联关系
- **所属服务**:[[svc_pbs]](= `related_services`)。
- **本库真实表**:见下表(= `related_tables`,共 26 张,均有独立表对象)。
- **谁读写它**:费率/计费在交易计费及账单核算中取数,见 [[tbl_trade_db]]、[[tbl_statement_db]]。
- 导航入口见 [[ts_payment_db_navigation]]。

## 本库表清单(26)
| 表对象 |
| --- |
| [[tbl_pbsdb_leaf_alloc]] |
| [[tbl_pbsdb_tb_bill]] |
| [[tbl_pbsdb_tb_payment_order]] |
| [[tbl_pbsdb_tb_pbs_bill]] |
| [[tbl_pbsdb_tb_pbs_bill_detail]] |
| [[tbl_pbsdb_tb_pbs_bill_strategy]] |
| [[tbl_pbsdb_tb_pbs_bill_workorder]] |
| [[tbl_pbsdb_tb_pbs_cachae_log]] |
| [[tbl_pbsdb_tb_pbs_cal_vat_config]] |
| [[tbl_pbsdb_tb_pbs_err_log]] |
| [[tbl_pbsdb_tb_pbs_error_monitor]] |
| [[tbl_pbsdb_tb_pbs_fee_assign]] |
| [[tbl_pbsdb_tb_pbs_fee_assign_detail]] |
| [[tbl_pbsdb_tb_pbs_fee_shared_strategy]] |
| [[tbl_pbsdb_tb_pbs_machine_monitor]] |
| [[tbl_pbsdb_tb_pbs_price_cal]] |
| [[tbl_pbsdb_tb_pbs_price_cal_range]] |
| [[tbl_pbsdb_tb_pbs_price_strategy]] |
| [[tbl_pbsdb_tb_pbs_price_strategy_detail]] |
| [[tbl_pbsdb_tb_pbs_price_strategy_log]] |
| [[tbl_pbsdb_tb_pbs_price_strategy_param]] |
| [[tbl_pbsdb_tb_pbs_price_strategy_unit]] |
| [[tbl_pbsdb_tb_pbs_request_log]] |
| [[tbl_pbsdb_tb_pbs_strategy_log]] |
| [[tbl_pbsdb_tb_trade_info]] |
| [[tbl_pbsdb_tm_bill_config]] |

## 校验点(QA 关注)
- 字段级以各表对象为准;此页仅作库内导航。
