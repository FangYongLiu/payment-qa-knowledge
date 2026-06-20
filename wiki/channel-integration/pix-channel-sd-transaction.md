---
title: PIX渠道SD交易设计说明
domain: channel-integration
kind: wiki_page
slug: pix-channel-sd-transaction
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:PMDPayment/490373264
tags: []
---

# PIX渠道SD交易设计说明

本页说明 PIX 渠道在 SD（收单/交易）侧的数据库结构与交易状态机流转，涵盖交易（Trade）与退款（Refund）两类交易的状态定义。

## 数据库（Database）

PIX 渠道 SD 交易相关的数据库表结构（详见原文附图 `image-20240516-092107.png`）。

## 状态机（Status Machine）

PIX 渠道 SD 侧的状态机分为两类：

- 交易状态机（Trade Transaction Status）
- 退款状态机（Refund Transaction Status）

### 交易状态（Trade Transaction Status）

PIX 交易类的状态流转（详见原文附图 `image-20240516-085438.png`）。

### 退款状态（Refund Transaction Status）

PIX 退款类的状态流转（详见原文附图 `image-20240516-085501.png`）。

---

> 说明：原文中数据库结构与状态机的具体字段、状态值与流转路径以图片形式呈现，本页保留章节框架；具体内容请参照原始设计文档中的对应图示。
