---
title: 付款码线下收单总览
domain: acquire-transaction
kind: wiki_page
slug: payment-code-offline-acquiring-overview
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki
source_ref: wiki:10a58f75-8c75-415a-9468-14c295644f8e
tags: []
---

# 付款码线下收单总览

付款码线下收单是用户出示付款码、由商户侧扫码完成收单的被扫支付模式，包含 POS 机扫码与扫码枪扫码两种场景。

## 被 POS 机扫

- **背景**：线下收单方式之一。用户出示付款码，商户使用 smart POS 扫码完成收单交易。
- **交易流程**：商户通过 smart POS 扫描用户付款码后发起收单交易。

## 被扫码枪扫

- **背景**：线下收单方式之一。用户出示付款码，商户使用扫码枪等扫码设备扫描付款码并解析。
- **交易流程**：商户后端调用 SGS 下单接口完成收单交易。

## 场景对比

| 场景 | 扫码设备 | 收单调用方式 |
| --- | --- | --- |
| 被 POS 机扫 | smart POS | POS 直接发起收单交易 |
| 被扫码枪扫 | 扫码枪等扫码设备 | 商户后端调 SGS 下单接口 |
