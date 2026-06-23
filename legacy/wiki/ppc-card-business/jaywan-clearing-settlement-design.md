---
title: Jaywan清算与结算设计
domain: ppc-card-business
kind: wiki_page
slug: jaywan-clearing-settlement-design
status: archived
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:PMDPayment/877428845
tags: []
---

# Jaywan清算与结算设计

本页聚焦 Jaywan 预付卡的清算文件处理、结算文件生成与对账流程的设计方案，属于 Phase 1 范围，承接 [[jaywan-system-design-phases]] 的整体规划，业务上属于 [[domain_jaywan_prepaid_card]]。

## 设计范围概览

清算与结算模块独立于交易主流程，主要处理 Dgpay 下发的 Clearing File，并由本侧生成 Settlement File，同时与 CS 团队对齐对账规则。

设计文档：`gppc-SD-Jaywan Clearing & Settlement`。

## 任务拆分与优先级

| Case | Dgpay API | 说明 | Priority | Workload | Developer |
|---|---|---|---|---|---|
| Clearing file process frame | Clearing File | 清算文件处理框架；同步落地 `DECLINE` 类型清算明细处理；在已有流程中追加 settlement 明细生成 | 0 | 2d | yu.tang |
| Clearing detail process - OFFLINE | - | `OFFLINE` 类型清算明细处理 | 1 | 1d | yu.tang |
| Clearing detail process - PROVISION, BALANCE_INQUERY | - | `PROVISION`、`BALANCE_INQUERY` 类型清算明细处理 | 1 | 2d | yu.tang |
| Clearing detail process - REVERSAL | - | `REVERSAL` 类型清算明细处理；对单条消息冲正补充 reverse settlement 更新 | 2 | 3d | yu.tang |
| Settlement file generation | Settlement File | 在单条消息流程中追加 settlement 明细生成；汇总输出 settlement 文件 | 3 | 2d | yu.tang |
| Reconciliation | - | 与 CS 团队对齐对账规则；在已有流程中接入对账信息发送 | 4 | 2d | yu.tang |

## 清算文件处理（Clearing File）

- 整体作为统一的处理框架先行落地（Priority 0），再按明细类型逐步扩展。
- 支持的清算明细类型：
  - `DECLINE`（与框架同期落地）
  - `OFFLINE`
  - `PROVISION`
  - `BALANCE_INQUERY`
  - `REVERSAL`：除了清算明细处理外，还需在单条消息冲正流程中补充反向 settlement 明细的更新。
- 处理思路：在已有的交易/冲正等单条消息流程中，扩展产生对应的 settlement 明细，使清算与单条消息侧数据保持一致。

相关交易侧实现见 [[jaywan-dgpay-integration-guide]]（Provision / Reversal / Balance Inquiry / Declined Transaction）。

## 结算文件生成（Settlement File）

- 在单条消息处理流程中嵌入 settlement 明细的生成逻辑。
- 在此基础上汇总输出 Settlement File。
- 优先级 3，依赖清算各明细类型处理已落地。

## 对账（Reconciliation）

- 需与 CS 团队对齐具体对账规则后再实现。
- 在已有流程中追加将对账所需信息发送出去的环节。
- 优先级 4，作为清算结算链路的最后一步。

## 与供应商的职责分工

来自供应商 Q&A（详见 [[jaywan-vendor-qa]]）：

- **Settlement**：由 Mbank 与 Botim 共同管理。
- **Reconciliation**：由 Botim 负责；若余额由 Botim 持有，SWITCH 到 host 的对账活动也由 Botim 完成。
- **Reports/formats**：Settlement 与 Clearing 的报文/文件格式由 Dgpay 侧提供给 Botim。
- **余额同步**：若 Botim 持有余额，则 Dgpay 侧不维护余额，无需 balance sync；相关接口 `UpdateCardBalance` 在该模式下不需要。

## 关联与上下游

- 上游交易消息：`provision`、`reversal`、`balance-inquiry`、`declined-transaction` 等 Institution API，详见 [[jaywan-dgpay-integration-guide]]。
- 项目背景与整体范围参见 [[jaywan-prepaid-card-overview]]。
- 阶段安排参见 [[jaywan-system-design-phases]]。
- 产品侧相关问题参见 [[jaywan-product-qa]]。
