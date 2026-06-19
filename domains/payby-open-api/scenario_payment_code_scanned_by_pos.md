---
id: scn_payment_code_scanned_by_pos
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
- POS
- 线下收单
subdomain: null
module: null
sensitivity: normal
name: 付款码被POS机扫场景
aliases: []
related_services:
- SGS
- acquire
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
- 商户后端已对接 SGS 下单接口，并具备接收异步通知的能力。

## 操作步骤
1. 用户出示付款码。
2. 商户使用 smart pos 扫描并解析用户的付款码。
3. 商户后端 → SGS：请求下单接口，传入解析得到的用户付款码。
4. SGS → acquire：转发请求下单接口。
5. acquire → SGS：返回下单结果。
6. SGS → 商户后端：返回下单结果（同步响应链路完成）。
7. acquire → SGS：异步通知支付结果。
8. SGS → 商户后端：异步通知支付结果。

## DB 校验点
原文未提供。

## 预期结果
- 同步链路：商户后端通过 SGS 调用 acquire 下单成功，并拿到下单结果。
- 异步链路：acquire 通过 SGS 将最终支付结果异步回传给商户后端。
- SGS 在整个流程中作为商户后端与 acquire 之间的中介/代理，完成 smart pos 扫付款码方式的线下收单交易。
