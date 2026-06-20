---
title: Jaywan mBank Botim卡 - 费用、Chargeback与UAT
domain: ppc-card-business
kind: wiki_page
slug: jaywan-mbank-fees-chargeback-uat
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_attachment
source_ref: wiki_attachment:c35b0d12-9994-4698-ad4e-538e1511baa7
tags: []
---

# Jaywan mBank Botim卡 - 费用、Chargeback与UAT

本页汇总 Botim Jaywan 卡（Powered by mBank）在交换费/退款、Chargeback、附加费用以及 UAT 环境方面的关键约定。对账与结算细节见 [[jaywan-mbank-reconciliation-settlement]]，门户与报表见 [[jaywan-mbank-botim-portal-and-reports]]，Chargeback 通用业务背景见 [[domain_chargeback]]。

## 交换费（Interchange）与 MCC

- 不同 MCC 对应的 Interchange 费率由 **Jaywan scheme** 规定，详见 Jaywan manual。
- Interchange 信息会按交易在对账报告中体现（参见 Clearing Report 中的 `Interchange Recon Fee Amount`、`Interchange Percentage`）。

## 退款与 IRF 回收

- 当一笔交易发生 refund 时：
  - **IRF 同步被回收**（debited）回 Mbank/Botim；
  - 同时会**收取 processing fee**。

## VAT 处理

- POS 交易的 IRF **不收取 VAT**。
- ATM 手续费向持卡人收取的 VAT，会**透传到 customer account**。

## Chargeback 流程

- 由 Botim 提出，**Mbank Operations 负责向 Mbank/CBUAE 侧发起 chargeback**。
- 实际操作在 **CBUAE Portal** 完成，由 Mbank processing team 使用；Astratech 是否需要 CBUAE Portal 访问权限待确认。
- **SLA 基于交易量另行定义**（提出与解决的具体时限待定）。

## Chargeback 与对账/结算的关系

- Chargeback **包含在对账文件中**，但与普通交易**单独展示**（同一份 settlement file 内分开列示）。
- Chargebacks & Fee **不会单独出文件**。
- 结算层面，chargeback **与正常交易分开结算**（refund、cancellation、declined 仍在同一 settlement file 中，详见 [[jaywan-mbank-reconciliation-settlement]]）。

## 附加费用（Project Fee 等）

- 除 interchange 之外**存在其他费用**（如 project fee），具体在商务条款（commercials）中细化。
- 此类附加费用**单独开票（Invoiced separately）**，**不从结算账户扣除**。

## UAT 与样本文件

- **暂无 UAT 环境**可供测试 reconciliation 与 settlement 流程；若 Scheme 提供，则 Mbank 可同步提供。
- Mbank 可**提供 Mbank recon file 格式样本**用于参考。
- 当前对账文件为 Excel 格式，会针对 Astratech 做客户化调整。
