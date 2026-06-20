---
title: WeChat海外用户主扫静态码支付流程
domain: channel-integration
kind: wiki_page
slug: wechat-overseas-static-qr-payment-flow
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:2f2ede24-4564-4541-814c-3df23ad70d8c
tags: []
---

# WeChat海外用户主扫静态码支付流程

本页描述海外钱包用户使用钱包客户端主动扫描 WeChat 商户静态二维码，完成商户识别、订单查询与支付确认的端到端交互流程。

## 参与方

- **User**：发起扫码与支付的最终用户
- **Overseas wallet client**：海外钱包客户端
- **Overseas wallet**：海外钱包后台
- **TenpayGlobal**：财付通海外侧
- **EPCC**：渠道清算/转接节点
- **WeChat Pay**：微信支付
- **Merchant backend**：商户后台

## 阶段一：扫码与商户识别（QR Scanning & Validation）

用户扫描 WeChat 商户静态码后，由海外钱包识别二维码类型并向 WeChat Pay 侧反查商户信息，但此时尚无订单信息。

时序步骤：

1. User → Overseas wallet client：使用钱包客户端扫描 WeChat 商户二维码
2. Overseas wallet client → Overseas wallet：提交扫码结果
3. Overseas wallet → TenpayGlobal：识别为 WeChat 二维码，调用商户码查询 `[QUERY_MERCHANT_CODE]`
4. TenpayGlobal → EPCC：查询商户订单 `[epcc.305.001.01]`
5. EPCC → WeChat Pay：查询商户订单 `[epcc.305.001.01]`
6. WeChat Pay → EPCC：商户订单回执 `[epcc.306.001.01]`
7. EPCC → TenpayGlobal：商户订单回执 `[epcc.306.001.01]`
8. TenpayGlobal → Overseas wallet：返回商户详情（无订单信息）
9. Overseas wallet → Overseas wallet client：返回商户详情
10. Overseas wallet client → User：展示商户信息

## 涉及报文与接口

- `QUERY_MERCHANT_CODE`：海外钱包向 TenpayGlobal 发起的商户码查询
- `epcc.305.001.01`：商户订单查询请求（TenpayGlobal ↔ EPCC ↔ WeChat Pay）
- `epcc.306.001.01`：商户订单查询回执（WeChat Pay ↔ EPCC ↔ TenpayGlobal）

## 阶段二：支付确认（Payment）

用户在确认商户信息后输入支付金额并确认支付，由钱包客户端提交支付请求至海外钱包，并继续向 TenpayGlobal 侧发起后续支付流程。

> 注：原文该阶段时序在 "Overseas wallet → Tenpay" 处截断，后续报文与回执细节以完整原始资料为准。
