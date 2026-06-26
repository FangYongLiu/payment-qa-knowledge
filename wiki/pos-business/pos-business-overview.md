---
title: POS业务总览
domain: device-pos
kind: wiki_page
slug: pos-business-overview
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:AQ/1135378560
tags: []
related_services:
  - svc_acquireii
  - svc_adtaxi
  - svc_device
related_tables:
  - tbl_active_code
  - tbl_device_apply_order
  - tbl_device_db
  - tbl_hardware_info
---

# POS业务总览

PayBy POS 业务覆盖多种设备形态与商户场景，包含自营 POS、为 ADCB 定制的 POS、出租车专用设备及虚拟 POS 等，涉及设备激活、密钥注入、产品开通、渠道报备和交易等完整流程。

## 设备类型分类

- **PayBy POS**：公司自营 POS 机，支持刷卡、扫码、发送 paylink
- **ADCB POS**：为 ADCB 定制的 POS 机，无资金流，不涉及资金结算与对账，兼容两种类型设备
  - **Taxi POS**：阿布扎比出租车上使用，设备类型为 P2 Mini，无打印设备
  - **Standard POS**：ADCB 商户使用
- **Virtual POS**：装在安卓手机上使用，只支持扫码、发送 payLink
- **Smart POS**：公司自营 POS 机，支持扫码、发送 paylink

## 功能差异对比

| 设备类型 | 刷卡 | 扫码 | PayLink | 打印 | 资金流 |
|---|---|---|---|---|---|
| PayBy POS | ✓ | ✓ | ✓ | — | 有 |
| Smart POS | — | ✓ | ✓ | — | 有 |
| Virtual POS | — | ✓ | ✓ | — | 有 |
| ADCB Taxi POS（P2 Mini） | — | — | — | 无 | 无 |
| ADCB Standard POS | — | — | — | — | 无 |

> ADCB POS 系列不涉及资金结算与对账。

## 涉及流程

POS 业务通用流程包括：

1. **设备激活**（通用）
2. **密钥注入**
3. **产品开通**
4. **渠道报备**
5. **做交易**
