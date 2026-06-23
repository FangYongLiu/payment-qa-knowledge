---
title: Jaywan产品矩阵与产品设置
domain: ppc-card-business
kind: wiki_page
slug: jaywan-product-matrix-and-setup
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_attachment
source_ref: wiki_attachment:e3c2c891-c5e7-47d3-9cfb-05825c9af14a
tags: []
---

# Jaywan产品矩阵与产品设置

本页聚焦Jaywan预付卡的产品矩阵定义、卡片个性化设计、BIN与产品参数配置，以及费率与限额设置。其他流程参见 [[jaywan-prepaid-card-brd-overview]]。

## 卡设计与个性化 (Card Design and Personalization)

- 遵循 Jaywan guidelines（待接收）
- Eproof approval（电子样稿审批）
- Card plastic specification（待接收）
- 个性化字段 (Personalization fields)：
  - Card（卡面）
  - Welcome letter（欢迎信）

## 产品设置 (Product Setup)

核心配置项：

- **BIN Configuration**：BIN配置
- **Program definition**：项目定义
- **Product type definition**：产品类型定义
- **Currency**：AED
- **Pin try limit**：3
- **Card generation Method**：random
- **PIN Delivery Method**：Green
- **Card Expiry Method**：5 Years – MM/YY
- **Plastic code**：塑料卡代码

## 费率设置 (Fee Setup)

按产品配置费用规则（具体费项以最终产品手册为准）。

## 限额管理 (Limit Management)

按产品维度进行限额配置；与交易权限（ECOM/POS/ATM）和MCC限制的动态控制相关，详见 [[jaywan-card-integration-scope]]。

## 产品类型支持

- 虚拟卡 (Virtual Card)
- 实体卡 (Physical Card)
- 两类卡均通过Botim app发行，支持完整生命周期

## 相关依赖

- MBank 需为 Astratech program 启用 BIN
- Product setup 列入部署前置 Action Points，详见 [[jaywan-uat-deployment-dependencies]]
- 业务域归属参见 [[domain_ppc_card_business]]
