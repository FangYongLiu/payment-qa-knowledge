---
id: flow_fiserv_pos_payment
object_type: Flow
domain: payby-authorization-protocol
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: wiki
source_ref: confluence:AQ/2199912473
tags:
- fiserv
- pos
- payment
subdomain: null
module: qpay-fsii
sensitivity: normal
name: Fiserv POS刷卡交易流程
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
POS设备完成Fiserv渠道绑定后，通过POS刷卡触发的交易支付链路。qpay-fsii从有效的ping_url中选取响应最快的URL发送交易报文，完成支付请求。

## 步骤(跨系统)
1. POS上点击下单：此操作不调用任何接口。
2. POS刷卡：
   - 先调用下单接口，得到订单 `tokenUrl`。
   - 然后自动调用支付接口。
3. qpay-fsii 收到交易请求后：
   - 从 `fiserv.t_ping_url` 中筛选有效的ping_url（要求 update_time 在最近6小时之内）。
   - 在有效ping_url中选取 `response_time_ms` 最小（速度最快）的那一个。
   - 向该 ping_url 发送交易报文，完成与Fiserv的支付通信。

## 涉及服务/表
- 服务：qpay-fsii
- 表：
  - `fiserv.t_ping_url`：存储4个 ping_url 及其 ping 响应时间，用于交易时选路。

## 校验点
- ping_url 有效性：仅 update_time 在最近6小时内的记录视为有效（Fiserv要求每6小时重新获取一次ping_url）。
- 选路规则：在有效ping_url中按 `response_time_ms` 最小者优先。
- 前置条件：设备已完成渠道绑定（device.t_fiserv_out_bound 状态为 ACTIVED，device.t_device_channel 已有 device_id 与 TID 的关联记录）。
