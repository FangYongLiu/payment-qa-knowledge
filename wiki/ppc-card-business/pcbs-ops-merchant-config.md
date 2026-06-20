---
title: PCBS运营商户配置(Card Processor与Partner)
domain: ppc-card-business
kind: wiki_page
slug: pcbs-ops-merchant-config
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:PMDPayment/845250859
tags: []
---

# PCBS运营商户配置(Card Processor与Partner)

记录 NymCard 作为 Card Processor 的日报文件 SFTP/UFS 路径规范，以及 Nublo 合作伙伴在不同 Wallet 下的商户 ID 映射。

## Card Processor: NymCard

| 项 | 值 |
|---|---|
| Processor | NymCard |
| SFTP user | `nymcard_01` |
| PCBS user | `binsponsorship_sftp` |

### SFTP 文件路径

```
/outfile/binsponsorship/${partnerCode}/${year}/Daily Balance Report-${date}.csv
```
（TODO：待确认）

参数说明：
- `${partnerCode}`：partner 标识
- `${year}`：文件所属年份
- `${date}`：文件日期

示例：
```
/outfile/binsponsorship/nublo/2024/Daily Balance Report-20241129.csv
```

### UFS 文件路径

```
/pcbs/daily-balance-report/${processorCode}/${partnerCode}/${year}/${fileName}
```

参数说明：
- `${processorCode}`：processor 标识
- 其余参数同上

示例：
```
/pcbs/daily-balance-report/nymcard/nublo/2024/Daily Balance Report-20241129.csv
```

## Partner under NymCard：Nublo 商户映射

按 Wallet 用途划分商户：

- **Wallet A、B merchant**：用于 Prefund 与 Escrow
- **Wallet D merchant**：用于 Loading from Lean and PG
- **Wallet C merchant**：用于 Profit

Nublo 在各 Wallet 下的 Merchant ID：

| Wallet | 用途 | UAT | PROD |
|---|---|---|---|
| Wallet A、B | Prefund and Escrow | `200000081147` | TODO |
| Wallet D | Loading from Lean and PG | `200000081148` | TODO |
| Wallet C | Profit | Phase 2 | Phase 2 |
