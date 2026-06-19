---
id: scn_payment_code_scanned_by_scanner
object_type: Scenario
domain: payby-open-api
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-19'
source_type: wiki_image
source_ref: wiki_image:d68f2e06-9802-4f50-a0e2-21f7afbe54b8
tags:
- 付款码
- 扫码枪
- 线下收单
subdomain: 付款码
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
- SGS 与 acquire 之间链路可用

## 操作步骤
1. 用户出示付款码
2. 商户使用扫码枪扫描付款码并解析
3. 商户后端 → SGS：请求下单接口，传入解析的用户付款码
4. SGS → acquire：请求下单接口
5. acquire → SGS：返回下单结果
6. SGS → 商户后端：返回下单结果
7. acquire → SGS：异步通知支付结果
8. SGS → 商户后端：异步通知支付结果

## DB 校验点
（原文未提供）

## 预期结果
- 同步流程：商户后端通过 SGS 调用 acquire 下单接口，获得下单结果
- 异步流程：acquire 通过 SGS 异步通知商户后端最终支付结果，完成线下收单交易
