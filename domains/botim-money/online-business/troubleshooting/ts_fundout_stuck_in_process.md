---
id: ts_fundout_stuck_in_process
object_type: Troubleshooting
name: 出款订单卡在处理中 (FundOut stuck IN_PROCESS) 的成因与人工处理
aliases: [fundout process, 出款处理中, 出款订单人工置结果, 退票]
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-07-03'
source_type: 有道云笔记(商户端2025) QA 实操整理
source_ref: 'PDF: 商户端系2025 (有道云笔记, 出款渠道失败/处理中处理, 2024-2025)'
tags: [online-business, fundout, troubleshooting, 对账, Counter]
related_services: [svc_merchant_fundout, svc_cmf, svc_counter]
related_scenarios: [scn_online_business_merchant_payout]
related_logs: []
---

# 出款订单卡在处理中 (FundOut stuck IN_PROCESS) 的成因与人工处理

## 症状
商户出款(fundout)订单长时间处于 **process / IN_PROCESS**,未终态成功或失败。

## 根因
渠道扣款可能成功、但返回失败/拒绝或无明确结果时,[[svc_cmf]] **默认把订单保持在 process**——除非渠道明确返回「失败」结果码,cmf 才判为 Failure;未明确的异常一律按处理中,**以避免资金亏损**(过早判失败会错误退款)。因此存在需人工确认的处理中订单。

## 人工处理 playbook(经 [[svc_counter]] 清算后台)
1. **置结果**:Counter → 渠道 → 订单管理 → 订单 → 置结果为「失败」或「成功」。
2. **审核**:Counter → 审核 → 审核列表 → 确认置结果的订单。
   - 更新渠道订单状态后,通知 [[svc_tradeii]] 更新订单状态,Acquire 变更订单最终状态;若置失败则账户资金发生退款。
3. **感知处理中订单的两条途径**:
   - 清算文件中有该 fundout 交易、而系统流水仍为 process → **对账失败**,人工确认并把渠道订单置为成功。
   - 系统流水一直 process 且无清算文件对账 → 渠道团队报表统计 process 笔数,通知产品/清算团队确认是否失败;确认失败则人工处理或出 **CR 批量**置失败(退款给商户)。

## 退票流程 (RefundTicket)
渠道退票时:Counter → 渠道 → 订单管理 → 订单 → 申请退票 → 审核(Counter → 审核 → 审核列表 → 详情)。
后端:`payment` 执行「出款退票-退票[551]」,`pfs-payment` 处理 `RefundTicketRequest`(`RefundSubmit→Refunded`),`dpm-accounting` 更新余额入账。

## QA 关注点
- 造「处理中」用例:出款金额落在 `10000–15000`(→ IN_PROCESS),见 [[reference_fundout_channel_mock_rules]]。
- 验证人工置结果后:订单终态、tradeii/Acquire 状态联动、置失败时账户退款金额正确。
- 对账驱动的处理中感知:清算文件有交易但流水 process → 对账应报差异。
- 退票后账户余额入账与订单状态一致。
