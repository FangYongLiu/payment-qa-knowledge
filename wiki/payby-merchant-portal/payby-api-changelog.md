---
title: PayBy接口文档变更记录
domain: merchant-portal
kind: wiki_page
slug: payby-api-changelog
status: active
owner: fangyong.liu@astratech.ae
reviewer: UNREVIEWED
source_type: upload
source_ref: api-docs/payby-api-v2.25-p3
tags: []
---

# PayBy接口文档变更记录

本页记录 PayBy 对外接口文档的版本迭代历史，按版本号、发布日期及主要变更点列出。

## 版本历史

| 版本 | 发布日期 | 主要变更 |
|------|---------|---------|
| v2.19 | 2024-06-27 | 创建订单请求新增 `subjectAr` |
| v2.20 | 2024-08-07 | 新增拒付通知 |
| v2.21 | 2024-09-18 | 新增 VAM 充值通知 |
| v2.22 | 2025-03-18 | 新增微信小程序支付 |
| v2.23 | 2025-04-15 | 新增 AFT 参数 |
| v2.24 | 2025-05-20 | DIRECTPAY 场景支持 DevicePay |
| v2.25 | 2025-10-23 | 新增预授权交易；查询、商户通知返回 Auth Code、RRN、Stan、Acquire Code、Acquire Message 信息 |

## 变更要点说明

### 订单与字段扩展
- **v2.19**：创建订单请求新增 `subjectAr` 字段。
- **v2.23**：新增 AFT 参数。

### 通知能力增强
- **v2.20**：新增拒付通知。
- **v2.21**：新增 VAM 充值通知。

### 支付场景扩展
- **v2.22**：新增微信小程序支付。
- **v2.24**：DIRECTPAY 场景支持 DevicePay。
- **v2.25**：新增预授权交易。

### 查询与回执信息丰富
- **v2.25**：查询接口和商户通知返回新增 Auth Code、RRN、Stan、Acquire Code、Acquire Message 等渠道信息字段。
