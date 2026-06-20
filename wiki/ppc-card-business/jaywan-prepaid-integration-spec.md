---
title: Jaywan预付卡新机构对接规范
domain: ppc-card-business
kind: wiki_page
slug: jaywan-prepaid-integration-spec
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:207380be-84c2-4326-80bf-928499d49050
tags: []
---

# Jaywan预付卡新机构对接规范

本页记录 Jaywan(dgpays) Prepaid Card 新机构对接文档（Prepaid New Institution Integration Document）的封面元数据与版本变更历史，作为后续接口与流程细节的总览入口。

## 文档元数据

- Document No: **DP.00001**
- First Publish Date: **21.05.2025**
- Revision Date: （空）
- Page No: 1
- 标题: **Prepaid Card - New Institution Integration Document**
- 当前版本: **Version 1.5**
- 归属系统: dgpays Prepaid

## 版本变更记录（Changelog）

| Version | Author | Changelog | Date |
|---|---|---|---|
| 1.0 | Gökhan Leblebici | First Draft | 21/05/2025 |
| 1.1 | Gökhan Leblebici | `RenewPrepaidCard`、`ReissuePrepaidCard`、`ReplacePrepaidCard` 服务的 `EmbossName` 入参发生变更；`GetPrepaidCardInfo` 方法的入参 `ClearCardNumber` 改为 `EncryptedCardNumber`；新增 `GetPrepaidCards`、`ResetPinRetryCount`、`ResetCvv2RetryCount` 方法 | 23/05/2025 |
| 1.2 | Gökhan Leblebici | provision、decline、reversal 方法新增 `clearingType` 入参；补充 clearing & settlement 流程说明与文件格式 | 29/05/2025 |
| 1.3 | Gökhan Leblebici | provision、balance inquiry、declined transaction 方法新增 `STAN` 与 `RRN` | 16/06/2025 |
| 1.4 | Gökhan Leblebici | provision 方法新增 `IsOfflineTrn` 标志位 | 05/08/2025 |
| 1.5 | Gökhan Leblebici | Rrn（原文未完整给出） | — |

## 关键变更主题速览

- **接口签名调整**：v1.1 调整发卡相关服务的 `EmbossName`，并将卡号入参由明文 `ClearCardNumber` 改为加密形式 `EncryptedCardNumber`。
- **新增管理类方法**：v1.1 新增 `GetPrepaidCards`、`ResetPinRetryCount`、`ResetCvv2RetryCount`。
- **清算与结算**：v1.2 在 provision / decline / reversal 引入 `clearingType`，并补充 clearing & settlement 流程及文件格式说明。
- **交易追踪字段**：v1.3 在 provision、balance inquiry、declined transaction 中加入 `STAN`、`RRN`。
- **离线交易支持**：v1.4 在 provision 中增加 `IsOfflineTrn` 标志。
- **v1.5**：与 `Rrn` 相关的进一步调整（原文截断，详见正式文档）。
