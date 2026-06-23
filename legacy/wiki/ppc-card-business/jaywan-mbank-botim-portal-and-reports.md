---
title: Jaywan mBank Botim卡 - 门户访问与报表需求
domain: ppc-card-business
kind: wiki_page
slug: jaywan-mbank-botim-portal-and-reports
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_attachment
source_ref: wiki_attachment:c35b0d12-9994-4698-ad4e-538e1511baa7
tags: []
---

# Jaywan mBank Botim卡 - 门户访问与报表需求

本页汇总 Astratech 内部客服与运营团队对 mBank 卡管理门户的访问诉求，以及在该门户上所需的各类报表清单与 mBank 的答复。费用、对账结算、Chargeback 等议题见 [[jaywan-mbank-fees-chargeback-uat]] 与 [[jaywan-mbank-reconciliation-settlement]]。

## 门户访问能力（Card Management Service Portal）

Astratech 客服与运营团队需要使用卡管理门户完成以下操作，mBank 答复如下：

- **卡片挂失/冻结（Blocking a card）**：mBank 将在 Portal 中启用并定制，作为项目交付项纳入 BRD。
- **查看用户交易历史（Viewing transaction history）**：支持，建议时间范围为 1 个月；需 Astratech 提供当前交易量及未来一年预测；将提供每日 dump 文件，Astratech 可导入自有 DWH/BI 工具。
- **发起 Chargeback（Raising chargebacks）**：在 CBUAE Portal 上完成，由 mBank 处理团队操作；如 Astratech 需直接访问 CBUAE Portal 请另行说明。详见 [[domain_chargeback]]。
- **Scheme 与 Processor 相关管理**：mBank 待确认（Please advise）。

## 门户演示与交付方式

- mBank 正在为 Portal 进行**定制化开发**；当前现有界面偏 Bank/Customer 视角。
- BRD 签署后可安排定制 Portal 的 demo（CMS demo 可先行）。
- BRD 中将包含：为 **Astratech BIN Range** 单独启用一套 Portal。

## 所需报表清单（Reports on the Portal）

mBank 答复：以下报表范围将在 BRD 中明确（To be scoped in the BRD）。

### Card Issuance Report（发卡报表）
- New Cards Report
- Replacements/Reissuance Report
- Card Closure Reports
- Active & Inactive Report
- Merchant Usage Report

### Daily Settlement Report（每日结算报表）
- Number of Transactions
- Settlement Currency
- Transactions Amount in Settlement Currency
- Interchange in Settlement Currency
- Billing Currency
- Cardholder Billing Amount

### Clearing Report（清算报表）
- Settlement Status
- Daily settlement count & spend
- Refund Count & spend
- Transaction Type
- Interchange Recon Fee Amount
- Interchange Percentage
- Transaction Settlement Currency：AED 与 NON-AED

### Authorization Report（授权报表）
- 每日交易总数（Total Number of transactions on daily basis）
- 成功交易数（Successful transaction count）
- 成功交易金额/Volume（Successful transaction spend）
- 拒绝交易报表（Decline transaction Report）
- 3DS Transaction report（如启用）

### Card Volume（卡量报表）
- Card Type：Virtual / Physical
- Total cards daily & monthly
- Total virtual cards daily & monthly
- Total Physical cards daily & monthly
- Total Active Cards monthly
- Apple token 总量（如启用）
- Google token 总量（如启用）

## 交易查询与授权流程确认

Astratech 的理解：所有交易的最终授权调用（final authorization call）由 Botim 完成——交易请求到达时，Botim 通过其风控引擎进行交易监控，必要时可拒绝/失败该交易。

- **mBank 答复**：确认需要 Botim 的响应；若 Botim 采用此流程，需将其纳入交易流并明确响应时间（response times），由 DGPAY 与 Botim 技术团队对接讨论。
