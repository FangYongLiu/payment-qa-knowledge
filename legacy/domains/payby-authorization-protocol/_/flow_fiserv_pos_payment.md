---
id: flow_fiserv_pos_payment
object_type: Flow
domain: authorization-protocol
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: wiki
source_ref: wiki:529d83bb-f8c0-47a4-af94-b05017e2e750
tags:
- fiserv
- pos
- payment
subdomain: null
module: qpay-fsii
sensitivity: normal
name: Fiserv POS刷卡支付流程
aliases: []
related_services: []
related_tables:
- tbl_fiserv_ping_url
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 概述
POS刷卡触发下单与支付接口的执行流程：POS点击下单时不调用任何接口，刷卡时先调下单接口拿到订单tokenUrl，再自动调支付接口；qpay-fsii收到交易请求后，从`fiserv.t_ping_url`中选择`response_time_ms`最小的ping_url发送交易报文。

## 步骤(跨系统)
1. POS上点击下单：不调用任何接口。
2. POS刷卡：
   - 先调用下单接口，得到订单`tokenUrl`。
   - 自动调用支付接口（携带`tokenUrl`发起支付请求）。
3. qpay-fsii 收到交易请求后：
   - 从`fiserv.t_ping_url`中筛选有效ping_url（仅`update_time`在最近6小时内的为有效）。
   - 在有效ping_url中选择`response_time_ms`最小（速度最快）的URL。
   - 请求该URL发送交易报文。

## 涉及服务/表
- 服务：qpay-fsii
- 表：`fiserv.t_ping_url`（用于选择最快的ping_url发送交易报文）

## 校验点
- POS点击下单阶段不应触发任何接口调用。
- 刷卡时下单接口需返回订单`tokenUrl`，随后才自动触发支付接口。
- qpay-fsii选取ping_url时，必须从`fiserv.t_ping_url`中按`response_time_ms`最小的记录选择。
- 仅`update_time`在最近6小时内的ping_url才视为有效（Fiserv要求每6小时重新获取一次ping_url）。
