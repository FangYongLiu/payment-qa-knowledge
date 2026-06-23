---
title: PIX渠道交易系统设计(数据库与状态机)
domain: channel-integration
kind: wiki_page
slug: pix-channel-transaction-design
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki
source_ref: wiki:d8c66de4-7927-4283-85dc-ae675e337408
tags: []
---

# PIX渠道交易系统设计(数据库与状态机)

本页概述 PIX 渠道交易模块的数据库结构与交易/退款状态机设计。

## 数据库

数据库结构以图示形式给出（参见原文 image-20240516-092107.png），用于支撑 PIX 渠道交易及退款相关的数据存储。

## 状态机

PIX 渠道交易模块包含两类状态机：

- Trade Transaction Status（交易状态机）
- Refund Transaction Status（退款状态机）

### Trade Transaction Status

交易流转的状态机定义，详见原文图示（image-20240516-085438.png）。

### Refund Transaction Status

退款流转的状态机定义，详见原文图示（image-20240516-085501.png）。

> 注：原文相关图片未能下载，具体字段、状态值与流转关系以源文档图示为准。
