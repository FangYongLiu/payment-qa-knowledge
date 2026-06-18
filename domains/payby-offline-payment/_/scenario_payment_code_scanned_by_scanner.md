---
id: scn_payment_code_scanned_by_scanner
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
- 扫码枪
subdomain: null
module: null
sensitivity: normal
name: 付款码被扫码枪扫场景
aliases: []
related_services: []
related_tables: []
related_scenarios:
- scn_payment_code_scanned_by_pos
related_logs: []
related_requirements: []
related_failures: []
---

## 触发/入口
用户出示付款码，商户使用扫码枪等扫码设备扫描付款码。

## 前置条件
- 用户已生成可用的付款码
- 商户具备扫码枪等扫码设备
- 商户后端可调用 SGS 下单接口

## 操作步骤
1. 用户出示付款码
2. 商户使用扫码枪扫描付款码并解析
3. 商户后端调用 SGS 下单接口进行收单交易

## DB 校验点
（原文未提供）

## 预期结果
通过 SGS 下单接口完成线下收单交易。
