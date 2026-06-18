---
title: PayBy接口协议规则
domain: payby-api-integration
kind: wiki_page
slug: payby-api-protocol-rules
status: active
owner: fangyong.liu@astratech.ae
reviewer: UNREVIEWED
source_type: upload
source_ref: api-docs/payby-api-v2.25-p4
tags: []
---

# PayBy接口协议规则

本页说明商户接入 PayBy 支付系统调用 API 时必须遵守的协议规则，涵盖传输、提交、数据格式、编码与签名等基础要求。相关支付场景定义见 [[payby-api-payment-scenarios]]。

## 协议规则一览

| 方式 | 说明 |
| --- | --- |
| 传输方式 | 为保证交易安全，采用 HTTPS 传输 |
| 提交方式 | 采用 POST 方法提交 |
| 数据格式 | JSON |
| 字符编码 | 统一采用 UTF-8 字符编码 |
| 签名算法 | SHA256WithRSA |
| 签名要求 | 请求和响应数据都需要签名 |

## 要点说明

- **传输方式**：必须使用 HTTPS，以保障交易安全。
- **提交方式**：仅支持 POST。
- **数据格式**：请求与响应均使用 JSON。
- **字符编码**：统一使用 UTF-8。
- **签名算法**：采用 SHA256WithRSA。
- **签名范围**：请求数据和响应数据双向均需签名。
