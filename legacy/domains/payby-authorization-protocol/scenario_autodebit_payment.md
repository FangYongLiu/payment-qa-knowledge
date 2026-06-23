---
id: scn_autodebit_payment
object_type: Scenario
domain: payby-authorization-protocol
status: archived
owner: wiki-sync@acquire
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-20'
source_type: wiki
source_ref: confluence:PMDPayment/702709784
tags:
- 代扣
- 授权支付
subdomain: null
module: null
sensitivity: normal
name: AutoDebit代扣支付场景
aliases:
- AUTODEBIT
related_services: []
related_tables: []
related_scenarios:
- scn_payandsign_payment
related_logs: []
related_requirements: []
related_failures: []
---

## 触发/入口
用户使用已生效的代扣协议号发起 AUTODEBIT 授权支付。

## 前置条件
- 已存在通过 PAYANDSIGN 场景生效的代扣协议号(协议号已通知给商户/用户)。
- 代扣协议处于生效状态。

## 操作步骤
1. 商户使用已生效的代扣协议号发起 AUTODEBIT 支付请求。
2. PayBy 依据代扣协议完成扣款。

## DB 校验点
原文未提供。

## 预期结果
使用已生效代扣协议号完成支付。
