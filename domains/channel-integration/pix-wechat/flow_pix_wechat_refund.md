---
id: flow_pix_wechat_refund
object_type: Flow
domain: channel-integration
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-20'
source_type: wiki
source_ref: wiki:a68e3cf4-694f-4d32-9a67-4b4aaeee8675
tags:
- refund
- wechat
- pix
- mpc
subdomain: pix-wechat
module: refund
sensitivity: normal
name: PIX微信退款流程
aliases: []
related_services: []
related_tables: []
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 概述
PIX 微信渠道退款采用同步发起 + 异步查询 + 推定成功机制。pix 系统作为 Responder 实现 REFUND 接口，发起退款时仅做必要校验后异步请求微信，立即返回 vendor 成功；微信侧无异步通知，由微信通过 QUERY_REFUND_ORDER_INFO 在 10 分钟内轮询退款状态；超过该时间窗口仍未拿到结果时，触发 NOTIFY_PRESUPPTIVE_REFUND_SUCCESS 推定退款成功，仅推定通知 1 次，一旦推定即按退款成功处理。钱包可通过次日账单获得推定的交易记录。退款允许失败。

## 步骤(跨系统)

### 1. 退款发起 (1.1 refund)
- 系统：pix
- 实现 vendor api：REFUND (Responder)
- 执行退款必要检查，异步请求退款，返回 vendor 成功（同步响应）
- 通知退款账单 (Notify refund bill)
- 退款金额计算规则：
  - Refund pay amount = Refund transaction amount / Original transaction amount * Original pay amount
- 参考系统设计：pix-SD-Transaction

### 2. 退款状态异步查询 (query refund)
- 系统：pix
- 实现 vendor api：QUERY_REFUND_ORDER_INFO (Responder)
- 在 10 分钟时间窗口内，由微信侧发起轮询查询退款状态

### 3. 退款推定成功 (notify final refund)
- 系统：pix
- 实现 vendor api：NOTIFY_PRESUPPTIVE_REFUND_SUCCESS (Responder)
- 触发条件：经过多次查询且长时间(10 分钟)无结果后执行推定
- 推定通知仅 1 次
- 一旦推定即按退款成功处理
- 钱包通过次日账单获得推定的交易记录

### 4. 账单与对账(other)
- 系统：pix → bill synchronization
- 系统：bill → bill configuration (UI/PRD)
- 系统：reconciliation → reconciliation configuration

## 涉及服务/表
- 服务：pix (pix-wechat)、bill、reconciliation、wallet(钱包侧通过次日账单获取推定记录)
- Vendor APIs：
  - REFUND (Responder)
  - QUERY_REFUND_ORDER_INFO (Responder)
  - NOTIFY_PRESUPPTIVE_REFUND_SUCCESS (Responder)
- 系统设计参考：pix-SD-Transaction

## 校验点
- 退款发起时执行必要的退款检查后再异步请求 vendor
- REFUND 接口仅有同步响应，无异步通知；状态需通过 QUERY_REFUND_ORDER_INFO 轮询
- 10 分钟为推定阈值：超过仍无结果才触发 NOTIFY_PRESUPPTIVE_REFUND_SUCCESS
- 推定通知只发 1 次，且推定后即按退款成功处理(不再回滚)
- 退款允许失败 (If refund fail allowed: Yes)
- 退款金额按比例换算：Refund pay amount = Refund transaction amount / Original transaction amount * Original pay amount
- 退款触发账单同步及对账(fundout/refund glide)流程
