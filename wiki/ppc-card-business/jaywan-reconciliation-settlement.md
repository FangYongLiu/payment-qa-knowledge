---
title: Jaywan对账与结算流程
domain: ppc-card-business
kind: wiki_page
slug: jaywan-reconciliation-settlement
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_attachment
source_ref: wiki_attachment:e3c2c891-c5e7-47d3-9cfb-05825c9af14a
tags: []
---

# Jaywan对账与结算流程

本页说明MBank（经Dgpays）向Astratech交付的T+1对账文件、AED日结算机制、advisement流程及争议处理时限。

## 对账文件交付

- **频率**：每日T+1生成对账文件
- **送达时间**：每日 04:00 AM GST 前可用
- **方式**：通过 SFTP 安全共享给 Astratech
- **格式**：Excel 或 CSV
- **覆盖窗口**：前一日 00:00–23:59 GST
- **时区**：所有时间戳统一使用 UAE GST

## 文件内容

对账文件须包含：

- Purchase Transactions
- Refund Transactions
- Declined Transactions
- Chargebacks（如适用）
- Authorizations（Success/Failure）
- Interchange and Fees

每笔交易须带唯一标识符（unique identifier），以支撑无原交易引用的退款等场景下的对账匹配。

## 结算机制

- **频率**：每日结算
- **周期**：T+1，基于前一日对账文件
- **结算币种**：Issuer Settlement Currency 为 **AED**
- **执行路径**：
  - Astratech 依据每日 advisement 在 MBank 预存资金（pre-fund）
  - MBank 通过 CBUAE 向 Jaywan Scheme 完成结算
  - Scheme Settlement 与 Internal Settlement 文件须对齐
- **方案分类**：所有交易须按 Jaywan 要求归类到对应 scheme code，以保证清分准确
- **退款与拒付处理**：以净额（net-off）方式在下一结算周期处理，或在当日文件中体现

## Advisement 流程

- 由 MBank Operations 每日向 Astratech 提供 advisement（具体时间待定）
- Advisement 须包含：
  - total debit
  - total credit
  - net position
  - currency breakdown

## 争议处理

- 对账文件中的任何差异，Astratech 须在**当日 14:00 GST 前**提出
- 除非争议获得书面确认，否则将按原文件继续完成最终结算

## 关联

- 文件落地与门户报表对应能力见 [[jaywan-portal-and-reporting]]
- 整体集成范围与上下文见 [[jaywan-card-integration-scope]] 和 [[jaywan-prepaid-card-brd-overview]]
- 结算流程的签核属于上线依赖，见 [[jaywan-uat-deployment-dependencies]]
