---
title: Jaywan清算与结算设计
domain: ppc-card-business
kind: wiki_page
slug: jaywan-clearing-settlement-design
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki
source_ref: wiki:b4ddb781-c8c9-4531-9714-54f78aa19fea
tags: []
---

# Jaywan清算与结算设计

本页聚焦 Jaywan 预付卡的 Clearing & Settlement 模块设计，包括清算文件处理框架、各类明细处理、结算文件生成与对账规则。相关上下文见 [[jaywan-phase1-system-design]] 与 [[jaywan-phase2-system-design]]，端到端流程见 [[flow_jaywan_card_lifecycle]]。

## 范围与定位

- 设计文档：gppc-SD-Jaywan Clearing & Settlement
- 与 Phase 1 的交易处理（Provision / Reversal / Balance Inquiry / Declined Transaction）联动，在已有流程上补充 settlement 明细生成与 reconciliation 流程。
- 用例总览参见 [[jaywan-use-case-list]]。

## Clearing 文件处理框架

- 处理对象：Dgpay 下发的 Clearing File。
- 框架职责：搭建清算文件的统一处理流程，并随框架同步落地 DECLINE 类型的清算明细处理。
- 在已有交易流程中追加 settlement 明细生成逻辑（即交易发生时即写入用于后续对账/结算的明细）。
- 优先级 P0，工作量约 2d。

## Clearing 明细处理

按明细类型分别实现处理逻辑：

- **OFFLINE**：离线交易明细的清算处理。优先级 P1。
- **PROVISION / BALANCE_INQUERY**：预授权/扣账类与余额查询类明细的清算处理。优先级 P1。
- **REVERSAL**：冲正明细的清算处理；同时为 single message reversal 增加 reverse settlement update（在单笔冲正发生时反向更新 settlement 数据）。优先级 P2。

对应的交易侧 Provision、Reversal、Balance Inquiry、Declined Transaction 实现见 [[jaywan-phase1-system-design]]。

## Settlement 文件生成

- 在 single message 类交易中追加 settlement 明细生成。
- 基于累计的 settlement 明细生成 Settlement File，对接 Dgpay Settlement File 规范。
- 优先级 P3。

## 对账（Reconciliation）

- 与 CS 团队对齐 reconciliation 规则后实现。
- 在已有交易流程中追加 reconciliation 流转（将交易记录纳入对账数据流）。
- 优先级 P4。

## Vendor 侧职责划分

来自 Dgpay 的确认（详见 [[jaywan-vendor-qa]]）：

- **Settlement**：由 Mbank 与 Botim 共同管理。
- **Reconciliation**：由 Botim 负责。
- **SWITCH 到 host 的对账**：若余额由 Botim 持有，则由 Botim 完成。
- Settlement 与 Clearing 的报表/文件格式由 Dgpay 提供给 Botim。
- 余额同步：Dgpay 侧可不维护余额，因此无需 balance sync（参考 UpdateCardBalance 相关说明）。

## 关联说明

- 产品总览：[[jaywan-prepaid-card-overview]]
- 产品 Q&A：[[jaywan-product-qa]]
- Vendor Q&A：[[jaywan-vendor-qa]]
