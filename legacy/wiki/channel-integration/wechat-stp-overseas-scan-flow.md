---
title: WeChat Pay 海外钱包主动扫静态码支付流程
domain: channel-integration
kind: wiki_page
slug: wechat-stp-overseas-scan-flow
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:d1e580fc-87d7-4725-95e7-341f015a7d03
tags: []
---

# WeChat Pay 海外钱包主动扫静态码支付流程

本页描述海外用户使用海外钱包客户端扫描微信商户静态二维码完成支付的端到端时序，分为扫码识别、支付通知、支付结果校验三个阶段。

## 参与方

- User
- Overseas wallet client
- Overseas wallet
- TenpayGlobal
- EPCC
- WeChat Pay
- Merchant backend

## 阶段划分

整体流程在时序图上划分为三段：

1. QR Scanning & Validation（扫码识别）
2. Payment Notification（支付通知）
3. Payment Validation（支付结果校验）

顶部的功能帧依次标注为：User scans code、Payment、Payment result synchronization。

## 阶段一：扫码识别（User scans code）

用户使用海外钱包扫描微信商户静态二维码，由海外钱包识别为微信码后，经 TenpayGlobal → EPCC → WeChat Pay 链路回查商户信息，但此阶段不返回订单信息。

时序步骤：

- User → Overseas wallet client：使用钱包客户端扫描 WeChat 商户二维码
- Overseas wallet client → Overseas wallet：提交扫码结果
- Overseas wallet → TenpayGlobal：识别为 WeChat 二维码，调用商户码查询 `[QUERY_MERCHANT_CODE]`
- TenpayGlobal → EPCC：查询商户订单 `[epcc.305.001.01]`
- EPCC → WeChat Pay：查询商户订单 `[epcc.305.001.01]`
- WeChat Pay → EPCC：商户订单回执 `[epcc.306.001.01]`
- EPCC → TenpayGlobal：商户订单回执 `[epcc.306.001.01]`
- TenpayGlobal → Overseas wallet：返回商户详情（不含订单信息）
- Overseas wallet → Overseas wallet client：返回商户详情
- Overseas wallet client → User：展示商户信息

## 阶段二：支付通知（Payment）

用户在钱包客户端确认金额后发起支付。（原文此处仅给出起始两步）

- User → Overseas wallet client：输入金额并确认支付
- Overseas wallet client → …（原文截断）

## 阶段三：支付结果校验（Payment Validation）

对应顶部 "Payment result synchronization" 帧，用于支付结果同步与校验。原文该阶段细节未在本片段中给出。

## 关键报文与接口

- `QUERY_MERCHANT_CODE`：海外钱包向 TenpayGlobal 发起的商户码查询接口
- `epcc.305.001.01`：商户订单查询报文（TenpayGlobal ↔ EPCC ↔ WeChat Pay）
- `epcc.306.001.01`：商户订单回执报文（WeChat Pay ↔ EPCC ↔ TenpayGlobal）
