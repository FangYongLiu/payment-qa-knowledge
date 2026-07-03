---
id: reference_jaywan_prepaid_card_overview
object_type: Reference
name: Jaywan预付卡项目总览
aliases: [jaywan-prepaid-card-overview]
domain: card
status: active
owner: jianfei.wang
reviewer: jianfei.wang
source_type: wiki
source_ref: confluence:PMDPayment/877428845
tags: [card, wiki-overview]
related_services: []
related_tables: []
---


# Jaywan预付卡项目总览

本页汇总 Jaywan 预付卡（通过 Dgpay 渠道接入）项目的整体背景、用例清单、阶段划分与参考资料，作为该业务域的入口页。详细设计、Q&A 见下方交叉链接。

参见业务域：domain_jaywan_prepaid_card。

## 项目背景与范围

- 渠道方：Dgpay（供应商），通过 Dgpays API 接入。
- 银行/发卡：Mbank；钱包/前台：Botim。
- 业务形态：虚拟卡 + 实体卡的预付卡（Prepaid Card）。
- 设计与对接细节：jaywan-dgpay-integration-guide。

## 参考资料

- Business Requirements Document
- Queries_Jaywan_mBank_Botim
- PRD（来自 Amir）
- Dgpays API Integration Documents（多份）
- UI 设计稿
  - 3.0.0 UI（Figma：Jaywan-Prepaid-Card）
  - 4.0.0 UI（Figma：My-Cards）
- Notifications 规范文档（SharePoint）

## 用例清单（Use Case）

按"Vendor API / Institution API / Priority"组织。Priority 数字越小越优先（0 为最高）。

### 通用 / 基础

| Case | Vendor API | Institution API | Priority |
|---|---|---|---|
| Common API Invoking | - | - | - |
| GetToken | GetToken | - | 0 |
| Institution Get Token | - | get-token | 2 |

### 虚拟卡

| Case | Vendor API | Priority |
|---|---|---|
| Create Virtual Card | CreatePrepaidDigitalCard（错误恢复：GetPrepaidCards） | 0 |
| View Card Detail | GetPrepaidCardInfo | 0 |
| Lock / Unlock Card, Replace Card, Close Card | UpdatePrepaidCardStatus | 0 |
| Reset PIN | PrepaidCardPinOperation | 0 |
| Auto sync mobile change | UpdateMobilePhoneNumber | 1 |
| Update Card Status from Bank Portal | - / update-prepaid-card-status | 3 |

### 实体卡

| Case | Vendor / Institution API | Priority |
|---|---|---|
| Apply Physical Card | CreatePrepaidEmbossData | 1 |
| Activate Physical Card | ActivatePrepaidCard | 1 |
| Delivery Tracking | notify-courier-process | 3 |

### 交易

| Case | Institution API | Priority |
|---|---|---|
| Transaction | provision | 2 |
| Transaction Reversal | reversal | 2 |
| Balance Inquiry | balance-inquiry | 2 |
| Declined Transaction | declined-transaction | 3 |

## 阶段划分（System Case）

完整阶段拆分、设计文档与工作量见 jaywan-system-design-phases。

- **Phase 1**：覆盖 Priority 0 / 1 / 2 用例，包括密钥管理、token 管理、虚拟卡申请/查询/PIN/锁卡解锁、实体卡申请与激活、Provision / Balance Inquiry / Reversal、Delivery tracking 等；以及 Priority 3 的若干恢复与状态同步项。
- **Clearing & Settlement**：清算文件处理框架，DECLINE / OFFLINE / PROVISION / BALANCE_INQUERY / REVERSAL 的清算明细处理，结算文件生成，与 CS 团队对齐对账规则。详见 jaywan-clearing-settlement-design。
- **Phase 2**：Replace Card、Close Card、Manual Release、ChargeFee（含 ChargeFeeCancel）、Pending Transaction Chasing 等。

## Q&A 索引

- 产品侧问题（虚拟卡 / 实体卡 / 交易 / 通知）：jaywan-product-qa
- 供应商 Dgpay 侧问题（通用、虚拟卡、实体卡、卡管理、余额同步、对账与结算等）：jaywan-vendor-qa
