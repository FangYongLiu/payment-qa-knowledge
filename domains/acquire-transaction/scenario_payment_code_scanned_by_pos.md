---
id: scn_payment_code_scanned_by_pos
object_type: Scenario
domain: acquire-transaction
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-19'
source_type: wiki_image
source_ref: wiki_image:aface4c4-573a-4862-bd4e-fa06bca60bc3
tags:
- 付款码
- POS
- 被扫
subdomain: null
module: null
sensitivity: normal
name: 付款码被POS机扫场景
aliases: []
related_services: []
related_tables: []
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 触发/入口
用户在结账时向商户出示付款码，商户使用 smart pos 扫码设备扫描该付款码以发起线下收单交易。

## 前置条件
- 用户已生成可用的付款码并展示。
- 商户具备 smart pos 扫码设备，可扫描并解析付款码。
- smart pos、pos-gateway、acquire 三方链路连通。

## 操作步骤
1. 用户出示付款码。
2. 商户使用 smart pos 扫描用户的付款码。
3. smart pos 扫码后向 pos-gateway 请求下单接口（扫码并请求下单接口）。
4. pos-gateway 将下单请求转发至 acquire（请求下单接口）。
5. acquire 处理下单后向 pos-gateway 返回下单结果。
6. pos-gateway 将下单结果返回给 smart pos。
7. smart pos 向 pos-gateway 发起轮询支付结果。
8. pos-gateway 将轮询请求转发至 acquire（轮询支付结果）。

注：图示中未画出轮询请求的响应箭头。

## DB 校验点
原文未提供。

## 预期结果
- smart pos 经由 pos-gateway 调用 acquire 完成下单，并能收到下单结果。
- smart pos 通过 pos-gateway → acquire 链路轮询支付结果，完成 smart pos 扫付款码的线下收单交易。
