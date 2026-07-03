---
id: svc_pbs
object_type: Service
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp003
name: pbs
dev_owner: Yadong.Lu
aliases: [gp003_pbs]
related_services: [svc_acs]
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

# pbs

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp003` · domain=`payment-core`。

## 作用
计费 / 定价（Pricing & Billing，pricingPayFee），调 acs

## 系统中的位置
- 功能层:出款 / 账务 / 对账 (Fundout / Accounting / Recon)
- 业务域:`payment-core`

## 关联关系
**调用(下游)—— 本服务依赖:**
- [[svc_acs]] acs（反欺诈 / 风控 + 渠道密钥） · 270003 次 · high

**被调用(上游)—— 这些服务调用本服务:**
fundout, offline-payment, tradeii, cashierii, cashdesk-api

## 参与的业务场景(cgs 回归)
- §1. 直连支付 / 预授权 / DCC（toB，`test_direct_pay` / `test_pre_auth_capture` / `test_bpg_paypage`）
- §2. 收银台 / 收银（`test_bpg_paypage` 收银侧、cashier 用例）
- §5. 银行/卡转账、出款（`test_transfer_to_bank` / `test_transfer_to_card`）

## 关键方法 / 入口(UAT 实测)
- `pricingPayFee`(`PayFeeRequest` → `FeeResponse`);交易/收银/出款下单时由 [[svc_tradeii]]/[[svc_cashierii]]/[[svc_cashdesk_api]]/fundout 调用算费。

## 涉及的 API / 数据库表
- **暴露/相关 API**:Dubbo `pricingPayFee`(算费);调 [[svc_acs]](商户费率/方案配置)。
- **读写的表**:费率/定价配置(具体对象待补)。

## 测试要点 / 排障 / 常见问题(UAT 实测)
- **算费口径**:pbs 计算 `payeeFeeAmount`(商户手续费),下游落 `t_payment_info`,并按 **VAT 公式** `pf_vat=round(payee_fee×5/105,2)`、`pfbt_amt=fee−pf_vat`、`settlement=paid−fee`(见 [[scn_online_business_cashier_pay]])。
- **怎么测/定位**:不同商户费率方案下 payeeFeeAmount 是否符合配置;费用与 [[svc_reconciliation]] calcFee、结算金额勾稽一致。
- 费率来源:acs 商户费率/方案配置。

## 相关流程 / 场景 / 排障(反向)
本服务涉及的流程/场景/排障(由对方 `related_services` 指向,反向汇总):
- [[flow_cashier_payment]](流程:收银台 / 收单卡支付端到端流程（含退款）)

## 来源与置信
- UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp003` · domain=`payment-core`。
