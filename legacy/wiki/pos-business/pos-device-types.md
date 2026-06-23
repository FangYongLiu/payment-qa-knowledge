---
title: POS设备类型与机型清单
domain: device-pos
kind: wiki_page
slug: pos-device-types
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki
source_ref: wiki:0ba653b7-9b7a-4d91-90fd-936ba14179ab
tags: []
---

# POS设备类型与机型清单

PayBy 现有 6 类 POS 形态，覆盖自营收单、ADCB 合作、出租车场景、虚拟终端等，不同形态在资金流、支持的支付方式、硬件能力上存在差异。相关业务背景见 [[pos-business-overview]]。

## PayBy POS
- 公司自营 POS 机
- 支持能力：刷卡、扫码、发送 paylink

## ADCB POS
- 为 ADCB 定制的 POS 机
- **无资金流**：不涉及资金结算与对账
- 兼容两种类型设备

## Taxi POS
- 部署场景：阿布扎比出租车
- 设备类型：P2 Mini
- 限制：**无打印设备**

## Standard POS
- 使用方：ADCB 商户

## Virtual POS
- 形态：装在安卓手机上使用的虚拟终端
- 支持能力：扫码、发送 payLink（不支持刷卡）

## Smart POS
- 公司自营 POS 机
- 支持能力：扫码、发送 paylink（不支持刷卡）

## 通用接入流程
所有设备类型均涉及以下环节：
- 设备激活（通用）
- 密钥注入
- 产品开通
- 渠道报备
- 做交易
