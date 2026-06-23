---
id: flow_pix_wechat_refund
object_type: Flow
domain: channel-integration
status: archived
owner: wiki-sync@acquire
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-20'
source_type: wiki
source_ref: confluence:PMDPayment/433881954
tags:
- refund
- wechat
- mpc
subdomain: pix-wechat
module: refund
sensitivity: normal
name: 微信渠道退款流程
aliases: []
related_services: []
related_tables: []
related_scenarios:
- REFUND
- QUERY_REFUND_ORDER_INFO
- NOTIFY_PRESUPPTIVE_REFUND_SUCCESS
related_logs: []
related_requirements: []
related_failures: []
---

## 概述
微信MPC渠道退款流程：由 pix 实现 vendor api，对退款做必要校验后异步发起退款请求，向 vendor 返回成功；微信侧对退款结果不提供异步通知，需通过 QUERY_REFUND_ORDER_INFO 在 10 分钟内主动查询；超过该时间窗口仍无结果时，调用 NOTIFY_PRESUPPTIVE_REFUND_SUCCESS 进行退款推定，默认仅推定通知 1 次，一旦推定即按退款成功处理。钱包侧可通过次日账单获取推定的交易记录。退款资金流通过 reconciliation 配置进行对账。

## 步骤(跨系统)
1. 1.1 refund — System: pix
   - 实现 vendor api（Responder: REFUND）
   - 做退款必要校验，异步请求退款，向 vendor 返回成功
   - 通知退款账单（Notify refund bill）
   - 退款金额计算：Refund pay amount = Refund transaction amount / Original transaction amount * Original pay amount
2. query refund — System: pix
   - 实现 vendor api：QUERY_REFUND_ORDER_INFO（Responder）
   - 查询本地退款状态；微信会在 10 分钟内通过该 API 查询退款结果
3. notify final refund — System: pix
   - 实现 vendor api：NOTIFY_PRESUPPTIVE_REFUND_SUCCESS（Responder）
   - 在多次查询且约 10 分钟仍无结果时执行推定；默认只推定通知 1 次，一旦推定按退款成功处理
4. bill synchronization (other) — System: pix
   - 退款账单同步
5. bill configuration (other) — System: bill
   - UI 与 PRD 配置（Owner: Yongxin Cao）
6. reconciliation configuration (other) — System: reconciliation
   - 退款相关对账配置（Owner: Yibin Xia）

## 涉及服务/表
- 服务：pix（pix-wechat）、bill、reconciliation
- Vendor API 场景：
  - REFUND（Responder）
  - QUERY_REFUND_ORDER_INFO（Responder）
  - NOTIFY_PRESUPPTIVE_REFUND_SUCCESS（Responder）
- 设计参考：pix-SD-Transaction
- 表：原文未提供

## 校验点
- 退款发起前需做必要校验（Do necessary check of refund）
- 退款金额换算公式：Refund pay amount = Refund transaction amount / Original transaction amount * Original pay amount
- 退款结果获取方式：无异步通知，依赖 QUERY_REFUND_ORDER_INFO 在 10 分钟窗口内查询
- 推定触发条件：经过多次查询且约 10 分钟仍无结果
- 推定通知次数：默认仅 1 次
- 推定结果处理：一旦推定即按退款成功处理，钱包通过次日账单获得推定交易记录
- 是否允许退款失败：Yes（If refund fail allowed？Yes）
