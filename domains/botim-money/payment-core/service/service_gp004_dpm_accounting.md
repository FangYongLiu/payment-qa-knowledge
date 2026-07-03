---
id: svc_dpm_accounting
object_type: Service
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp004
name: dpm-accounting
dev_owner: Cong.Zhou
aliases: [gp004_dpm-accounting]
related_services: []
related_tables:
- tbl_dpm_dbajobconf
- tbl_dpm_dbajoblog
- tbl_dpm_leaf_alloc
- tbl_dpm_t_act_account_titile
- tbl_dpm_t_compensation_event
- tbl_dpm_t_dpm_account_crl_def
- tbl_dpm_t_dpm_account_entry
- tbl_dpm_t_dpm_buffer_detail
- tbl_dpm_t_dpm_buffer_detail_log
- tbl_dpm_t_dpm_buffer_rule
- tbl_dpm_t_dpm_inner_account
- tbl_dpm_t_dpm_inner_account_detail
- tbl_dpm_t_dpm_inner_account_diary
- tbl_dpm_t_dpm_inner_sub_account
- tbl_dpm_t_dpm_inner_sub_account_his
- tbl_dpm_t_dpm_management_log
- tbl_dpm_t_dpm_outer_account
- tbl_dpm_t_dpm_outer_account_ctrl
- tbl_dpm_t_dpm_outer_account_detail
- tbl_dpm_t_dpm_outer_account_diary
- tbl_dpm_t_dpm_outer_account_status_his
- tbl_dpm_t_dpm_outer_account_sub_detail
- tbl_dpm_t_dpm_outer_account_subset
- tbl_dpm_t_dpm_pay_package
- tbl_dpm_t_dpm_pay_transaction
- tbl_dpm_t_job_progress
- tbl_dpm_tb_inner_account_daily
- tbl_dpm_tb_title_daily
- tbl_dpm_tb_title_daily_account
- tbl_dpm_tb_title_stat
- tbl_dpm_temp_trg_log
---

# dpm-accounting

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp004` · domain=`payment-core`。

## 作用
账务平台记账（DPM Accounting，被 member 调用）

## 系统中的位置
- 功能层:出款 / 账务 / 对账 (Fundout / Accounting / Recon)
- 业务域:`payment-core`

## 关联关系

**被调用(上游)—— 这些服务调用本服务:**
member

## 涉及的 API / 数据库表
- **暴露/相关 API**:Dubbo `[APP->DPM_V2]` 入账处理(`AccountingRequest`);被 [[svc_member]] / [[svc_payment]] 结算调入。
- **读写的表**:账户余额 / 入账流水(DPM 账户表,待补具体表名)。

## 关键方法 / 入口(UAT 实测)
- `[APP->DPM_V2]入账处理请求:AccountingRequest` → `准备开始更新余额,实时入账[N]条,缓冲入账[M]条` → `开始更新帐户余额[<accountNo>]` → `余额更新完成` → `[APPM<-DPM_V2]入账处理完成:AccountingResponse`。

## 测试要点 / 排障 / 常见问题(UAT 实测)
- **记账触发**:支付完成后 [[svc_payment]] `[OM-->DPM]结算请求` → dpm-accounting 实时入账更新余额;是资金最终落账环节。
- **怎么测/定位**:按 `paymentSeqNo`/结算号核对入账条数与余额变动;余额不一致时查"实时入账[N]条"是否与预期分录数吻合。
- 与 [[svc_reconciliation]] 对账勾稽:入账流水 vs 渠道清算流水。

## 相关流程 / 场景 / 排障(反向)
本服务涉及的流程/场景/排障(由对方 `related_services` 指向,反向汇总):
- [[flow_botim_transfer]](流程:BOTIM/ToC 转账与加款端到端流程)
- [[flow_cashier_payment]](流程:收银台 / 收单卡支付端到端流程（含退款）)
- [[flow_zand_fundout]](流程:ZAND渠道出款端到端流程(SP/SQ/VS))
- [[scn_online_business_zand_fundout]](场景:ZAND渠道出款测试场景(TC-001~010))

## 来源与置信
- UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp004` · domain=`payment-core`。
