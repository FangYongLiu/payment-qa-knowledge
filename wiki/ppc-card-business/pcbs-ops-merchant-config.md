---
title: PCBS运维商户配置(Card Processor与Partner)
domain: ppc-card-business
kind: wiki_page
slug: pcbs-ops-merchant-config
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki
source_ref: wiki:2e1ac663-d99e-4d73-b734-517c4bf66ad4
tags: []
---

# PCBS运维商户配置(Card Processor与Partner)

本页记录 PCBS 在 Card Processor 维度下的 SFTP/UFS 文件路径规范，以及 NymCard 下 Partner（Nublo）各钱包对应的商户号配置。

## Card Processor

当前已配置的 Processor 与对应账号：

| Processor | Sftp user | File path |
|---|---|---|
| NymCard | partner: `nymcard_01` | pcbs: `binsponsorship_sftp` |

### SFTP 路径

- 路径格式：`/outfile/binsponsorship/${partnerCode}/${year}/Daily Balance Report-${date}.csv`（TODO 待确认）
- 占位符说明：
  - `${partnerCode}`：partner 标识
  - `${year}`：文件所属年份
  - `${date}`：文件日期
- 示例：`/outfile/binsponsorship/nublo/2024/Daily Balance Report-20241129.csv`

### UFS 路径

- 路径格式：`/pcbs/daily-balance-report/${processorCode}/${partnerCode}/${year}/${fileName}`
- 占位符说明：
  - `${processorCode}`：processor 标识
  - 其余占位符同 SFTP
- 示例：`/pcbs/daily-balance-report/nymcard/nublo/2024/Daily Balance Report-20241129.csv`

## Partner under NymCard

NymCard 下 Partner = Nublo，按钱包用途划分商户号：

| Merchant | 用途 | UAT | PROD |
|---|---|---|---|
| Wallet A, B merchant | Prefund and Escrow | 200000081147 | TODO |
| Wallet D merchant | Loading from Lean and PG | 200000081148 | TODO |
| Wallet C merchant | Profit | Phase 2 | Phase 2 |

说明：
- Wallet A、B：Prefund 与 Escrow 共用同一商户号
- Wallet D：用于 Lean 与 PG 的 Loading
- Wallet C：Profit，UAT/PROD 均处于 Phase 2
