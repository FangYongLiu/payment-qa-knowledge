---
title: GPPC OP环境配置(Dgpay与gppc-jaywan API)
domain: ppc-card-business
kind: wiki_page
slug: gppc-op-env-configuration
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:PMDPayment/1143242758
tags: []
---

# GPPC OP环境配置(Dgpay与gppc-jaywan API)

本页汇总 GPPC OP 业务在 Dgpay 侧的费用收单商户号、集成网关 URL、产品号配置，以及 gppc-jaywan 对接 Dgpay 的机构 API 端点清单（覆盖 SIM/UAT/PROD 三套环境）。

## Dgpay 配置

### Fee Collection Merchant (Jaywan Fee Collection - Jaywan)

| 环境 | 商户号 |
|---|---|
| SIM | 200000433440 |
| UAT | 200000083365 |
| PROD | 200024937979 |

### New Account

- gppc-OP-Funds Flow

### Dgpay Integration 网关 URL

- SIM/TEST: `https://testmbankprepaid.dgpays.com/NetaIntegrationGateway/api/AstraTechIntegrationService/{{METHOD_NAME}}`
- UAT: `https://kongapi.mbankuae-uat.local:8443/uat/api/AstraTechIntegrationService/{{METHOD_NAME}}`

### 产品号配置

| Item | SIM | UAT | PROD |
|---|---|---|---|
| ProductNumber | 051 | 051 | 051 |
| SubProductNumber | 051 | 051 | 051 |

## Institution API: gppc-jaywan

### Url Prefix

| 环境 | Url Prefix |
|---|---|
| SIM | `https://sim-gppc-ext.test2pay.com/gppc-jaywan/api/dgpay/{UrlSuffix}` |
| UAT | `https://uat-gppc-ext.test2pay.com/gppc-jaywan/api/dgpay/{UrlSuffix}` |
| PROD | `https://gppc-ext.payby.com/gppc-jaywan/api/dgpay/{UrlSuffix}` |

### API 列表 (Url Suffix)

| API | Url Suffix |
|---|---|
| Get token | `/get-token` |
| Update prepaid card status | `/update-prepaid-card-status` |
| Provision | `/provision` |
| Balance inquiry | `/balance-inquiry` |
| Reversal | `/reversal` |
| Declined transaction | `/declined-transaction` |
| Notify courier process | `/notify-courier-process` |

PROD 完整地址示例：`https://gppc-ext.payby.com/gppc-jaywan/api/dgpay/{UrlSuffix}`，将 `{UrlSuffix}` 替换为上表对应路径即可（如 `/get-token` → `https://gppc-ext.payby.com/gppc-jaywan/api/dgpay/get-token`）。
