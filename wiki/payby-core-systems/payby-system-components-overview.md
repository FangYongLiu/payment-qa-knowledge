---
title: PayBy系统组件架构总览
domain: payby-core-systems
kind: wiki_page
slug: payby-system-components-overview
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:PCW/124553302
tags: []
---

# PayBy系统组件架构总览

PayBy 系统组件按职责自上而下划分为 Payment Product、Payment Core、Payment Public、Infrastructure 四个层次，分别承载支付产品能力、支付核心引擎、对外公共服务以及底层基础设施。

## 分层结构

- **Payment Product**：支付产品层，面向具体支付业务场景的产品组件。
- **Payment Core**：支付核心层，承载核心交易与账务相关能力。
- **Payment Public**：对外公共服务层，提供面向外部/通用的服务组件。
- **Infrastructure**：基础设施层，支撑上层业务运行的底层平台组件。

## Payment Product

支付产品层组件架构图（详见原文配图 `image2020-1-14_12-32-51.png`）。

## Payment Core

支付核心层组件架构图（详见原文配图 `image2021-6-21_11-18-53.png`）。

## Payment Public

支付公共层组件架构图（详见原文配图 `image2021-3-9_12-10-32.png`）。

## Infrastructure

基础设施层组件架构图（详见原文配图 `image2021-6-21_11-18-18.png`）。

> 备注：原文四层组件的具体清单以架构图形式给出，本页未文字化展开，详细组件请参阅对应架构图。
