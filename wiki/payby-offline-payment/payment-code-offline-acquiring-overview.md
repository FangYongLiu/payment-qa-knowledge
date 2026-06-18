---
title: 付款码线下收单总览
domain: payby-offline-payment
kind: wiki_page
slug: payment-code-offline-acquiring-overview
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:tester/124289143
tags: []
---

# 付款码线下收单总览

付款码线下收单是指用户出示付款码、由商户侧设备扫码完成收款的线下交易方式，主要包含 POS 机扫码与扫码枪扫码两种形态。

## 收单方式

线下付款码收单按商户扫码设备不同，分为以下两种场景：

- **被 POS 机扫**：用户出示付款码，商户使用 smart pos 扫码并完成收单交易。详见 [[scn_payment_code_scanned_by_pos]]。
- **被扫码枪扫**：用户出示付款码，商户使用扫码枪等扫码设备扫描付款码并解析，商户后端调 SGS 下单接口完成收单交易。详见 [[scn_payment_code_scanned_by_scanner]]。

## 交易流程

两种方式均遵循"用户出示付款码 → 商户侧扫码 → 发起收单"的基本链路，差异主要体现在扫码设备与下单发起方：

- POS 机扫：由 smart pos 直接完成扫码与收单交易。
- 扫码枪扫：扫码枪解析付款码后，由商户后端调用 SGS 下单接口发起收单。

具体的端到端时序与交互细节见各场景页。
