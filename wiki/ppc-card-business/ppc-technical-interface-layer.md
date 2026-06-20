---
title: PPC技术接口层总览
domain: ppc-card-business
kind: wiki_page
slug: ppc-technical-interface-layer
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki
source_ref: wiki:e1d88059-54cb-4219-a896-5486cad3e06d
tags: []
---

# PPC技术接口层总览

本页是 PPC 卡业务**技术接口层**的索引骨架，定义了接口契约、表结构与上下游依赖的范围与归集方式，供接口/集成测试用例生成参考。

## 本层用途

- 决定测试用例的"形态"：接口字段、数据库表结构、上下游依赖
- LLM 只有看到接口契约，才能生成可执行的接口/集成测试

## 应包含的内容

### 核心 API 清单
开卡、激活、查余额、查交易、冻结/解冻、挂失、补卡、销卡、换 PIN、查 CVV、3DS 验证

### 卡组织接口
- Mastercard MCAPI
- Jaywan 接口
- Sandbox 域名 / 证书

### 异步事件
- 授权报文
- 清算文件
- 退款回执
- 风控决策回调

### 关键表与字段
重点标注 **金额、状态、币种** 字段：
- `card`
- `card_account`
- `card_authorization`
- `card_clearing`
- `card_transaction`
- `card_dispute`

### 上下游依赖图
KYC、风控、账务、清结算、通知中心、汇率服务

## 数据来源

- 接口文档（apidoc / Yapi）
- 数据库 DDL
- 系统架构图（Confluence Pay Core Workspace）
- 接口联调文档

## 维护责任

- **主负责人**：Jianfei Wang
- **内容贡献**：建议每个接口由对应 owner 维护

## 状态

骨架（待补充）；子页见左侧页面树。
