---
id: domain_pos_business
object_type: Domain
domain: device-pos
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: wiki
source_ref: wiki:0ba653b7-9b7a-4d91-90fd-936ba14179ab
tags:
- POS
- 业务域
subdomain: null
module: null
sensitivity: normal
name: POS业务域
aliases: []
related_services: []
related_tables: []
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 概述
POS业务域覆盖 PayBy 体系下多种 POS 形态的整体业务，涵盖自营与合作伙伴场景，统一处理设备管理、产品开通与交易流程。

## 覆盖范围
按机型与归属划分，POS业务域包含以下类型：
- **PayBy POS**：公司自营 POS 机，支持刷卡、扫码、发送 paylink
- **ADCB POS**：为 ADCB 做的 POS 机，无资金流，不涉及资金结算与对账，兼容两个类型设备
- **Taxi POS**：阿布扎比出租车上使用，设备类型 P2 Mini，无打印设备
- **Standard POS**：ADCB 商户使用
- **Vitural POS**：装在安卓手机上使用，只支持扫码、发送 payLink
- **Smart POS**：公司自营 POS 机，支持扫码、发送 paylink

详见 [[pos-device-types]]。

## 关键服务/流程
本业务域涉及以下关键环节：
- 设备激活（通用）
- 密钥注入
- 产品开通
- 渠道报备
- 做交易

## QA 关注点
- 不同机型在交易能力上的差异：刷卡、扫码、paylink、是否带打印设备等需要按机型校验
- ADCB POS 无资金流，**不涉及资金结算与对账**，与 PayBy POS / Smart POS 的资金链路需区分
- Taxi POS 使用 P2 Mini 且无打印设备，相关交易凭证流程需注意
- Vitural POS 装在安卓手机上，仅支持扫码与 payLink，能力受限
- 设备激活、密钥注入、产品开通、渠道报备、交易五大流程在所有机型上的适配与回归

更多业务总览见 [[pos-business-overview]]。
