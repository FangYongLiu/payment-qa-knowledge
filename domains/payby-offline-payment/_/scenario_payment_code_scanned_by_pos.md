---
id: scn_payment_code_scanned_by_pos
object_type: Scenario
domain: payby-offline-payment
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: wiki
source_ref: confluence:tester/124289143
tags:
- 线下收单
- 付款码
- POS
subdomain: null
module: null
sensitivity: normal
name: 付款码被POS机扫场景
aliases: []
related_services: []
related_tables: []
related_scenarios:
- scn_payment_code_scanned_by_scanner
related_logs: []
related_requirements: []
related_failures: []
---

## 触发/入口
用户在结账时向商户出示付款码，商户使用 smart pos 扫码设备扫描该付款码以发起线下收单交易。

## 前置条件
- 用户已生成可用的付款码并展示。
- 商户具备 smart pos 扫码设备，可扫描并解析付款码。

## 操作步骤
1. 用户出示付款码。
2. 商户使用 smart pos 扫描用户的付款码。
3. smart pos 进入收单交易流程。

## DB 校验点
原文未提供。

## 预期结果
线下收单交易按 smart pos 扫付款码方式完成。

（说明：原文交易流程图未能下载，详细链路细节以图示为准。）
