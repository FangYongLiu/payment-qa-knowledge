---
title: POS业务总览
domain: pos-business
kind: wiki_page
slug: pos-business-overview
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki
source_ref: wiki:0ba653b7-9b7a-4d91-90fd-936ba14179ab
tags: []
---

# POS业务总览

PayBy 的 POS 业务涵盖多种机型，覆盖自营收单、银行合作、出租车场景及虚拟终端等不同业务形态，并共享一套通用的激活、密钥注入、产品开通、渠道报备与交易流程。

## 业务定位

POS 业务按机型与合作方划分为以下几类：

- **PayBy POS**：公司自营 POS 机，支持刷卡、扫码、发送 paylink
- **ADCB POS**：为 ADCB 定制的 POS 机，**无资金流**，不涉及资金结算与对账，兼容两类设备
  - **Taxi POS**：阿布扎比出租车上使用，设备类型为 P2 Mini，**无打印设备**
  - **Standard POS**：ADCB 商户使用
- **Virtual POS**：安装在安卓手机上使用，仅支持扫码、发送 payLink
- **Smart POS**：公司自营 POS 机，支持扫码、发送 paylink

各机型的设备型号细分见 [[pos-device-types]]。

## 通用业务流程

不同机型在业务上下文中均会涉及以下通用环节：

- **设备激活**（通用流程）
- **密钥注入**
- **产品开通**
- **渠道报备**
- **做交易**

## 资金流差异

- **有资金流**：PayBy POS、Virtual POS、Smart POS（涉及资金结算与对账）
- **无资金流**：ADCB POS（Taxi POS、Standard POS），不涉及资金结算与对账

## 相关

- 业务域归属：[[domain_pos_business]]
- 机型与设备类型清单：[[pos-device-types]]
