---
id: scn_payandsign_payment
object_type: Scenario
domain: payby-authorization-protocol
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-20'
source_type: wiki
source_ref: confluence:PMDPayment/702709784
tags:
- 支付场景
- 代扣签约
subdomain: null
module: null
sensitivity: normal
name: PayAndSign支付并签约场景
aliases:
- PAYANDSIGN
related_services: []
related_tables: []
related_scenarios:
- scn_directpay_first_and_subsequent
- scn_autodebit_payment
related_logs: []
related_requirements: []
related_failures: []
---

## 触发/入口
用户发起 PAYANDSIGN（支付并签约）类型的支付请求，在完成支付的同时认可代扣协议。

## 前置条件
- 用户具备可用支付卡，可完成本次支付
- 商户接入 PAYANDSIGN 场景，支持代扣协议生成

## 操作步骤
1. 用户发起 PAYANDSIGN 支付
2. PayBy 处理支付流程，用户完成支付即视为认可代扣协议
3. 支付成功后，PayBy 生成代扣协议并使其生效
4. PayBy 通过 notify 方式将协议号通知给用户/商户

## DB 校验点
- 代扣协议记录已生成且状态为生效
- 支付订单为成功状态

## 预期结果
- 用户完成支付
- 代扣协议生效，协议号回传商户
- 后续用户/商户可使用该协议号通过 AUTODEBIT 进行代扣支付
