---
id: svc_counter
object_type: Service
domain: settlement
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp031
name: counter
dev_owner: Yibing.Xia
aliases: [gp031_counter]
related_services: [svc_cards, svc_escrow, svc_vis, svc_router, svc_reconciliation, svc_dpm_accounting, svc_visii, svc_cmf]
related_tables: []
---

# counter

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp031` · domain=`payment-core`。

## 作用
账务记账（入账 Counter，被 payment 调用）

## 系统中的位置
- 功能层:出款 / 账务 / 对账 (Fundout / Accounting / Recon)
- 业务域:`payment-core`

## 关联关系
**调用(下游)—— 本服务依赖:**
- [[svc_cards]] cards（卡管理） · 3929 次 · high
- [[svc_escrow]] escrow（担保 / 托管交易） · 1454 次 · high
- [[svc_vis]] vis · 1215 次 · high
- [[svc_router]] router（渠道路由） · 1036 次 · high
- [[svc_reconciliation]] reconciliation（对账） · 743 次 · high
- [[svc_dpm_accounting]] dpm-accounting（账务平台记账） · 293 次 · high
- [[svc_visii]] visii · 12 次 · high
- [[svc_cmf]] cmf（渠道管理与资金） · 10 次 · high

**被调用(上游)—— 这些服务调用本服务:**
payment

## 参与的业务场景(cgs 回归)
- §1. 直连支付 / 预授权 / DCC（toB，`test_direct_pay` / `test_pre_auth_capture` / `test_bpg_paypage`）

## 涉及的 API / 数据库表
- **暴露 API**(Dubbo,来源 `counter-dubbo-api` 文档):`ChargeBackFacade`(拒付:`apply` / `query` / `update`)、`RefundTicketFacade`(退票:`applyRefundTicket` / `getRefundReason`)。另被 [[svc_payment]] 调做入账记账;清算后台操作(渠道订单管理/置结果/审核)。
- **读写的表**:清算/审核/渠道账户表(具体对象待补)。

## 关键方法 / 入口(UAT 实测)
- **入账记账**:被 payment 调,记账入账。
- **清算后台(人工运营)**:`收到请求 auditId=<...>`;渠道 → 订单管理 → **置结果**(成功/失败)→ 审核列表确认;**退票**:申请退票 → 审核 → payment 执行 `出款退票-退票[551]`。
- 查渠道账户:`Counter=>Payment ChannelAccount response`。

## 测试要点 / 排障 / 常见问题(UAT 实测)
- **处理中出款人工处理**:渠道返回失败/无结果时订单保持 process,经 Counter **置结果 + 审核**推终态(置失败则退款给商户);完整 playbook 见 [[ts_fundout_stuck_in_process]]。
- **退票**:Counter 申请退票 → 审核 → payment `[551]`;核对账户余额入账与订单状态一致。
- **怎么测/定位**:模拟渠道失败(金额区间/有效期 Mock,见 [[reference_fundout_channel_mock_rules]])→ 造 process 单 → Counter 置结果 → 验证 tradeii/Acquire 状态联动 + 资金回退。
- 与 [[svc_reconciliation]] 对账勾稽:清算文件有交易但系统流水 process → 对账差异 → 人工确认。

## 相关流程 / 场景 / 排障(反向)
本服务涉及的流程/场景/排障(由对方 `related_services` 指向,反向汇总):
- [[flow_cashier_payment]](流程:收银台 / 收单卡支付端到端流程（含退款）)
- [[flow_manual_fund_settlement]](流程:人工资金调拨端到端流程)
- [[scn_payment_core_manual_fund_settlement]](场景:人工资金调拨-产品码映射与资金流校验)

## 来源与置信
- UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp031` · domain=`payment-core`。
