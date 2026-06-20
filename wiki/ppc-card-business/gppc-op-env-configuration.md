---
title: GPPC OP环境配置(Dgpay与gppc-jaywan API)
domain: ppc-card-business
kind: wiki_page
slug: gppc-op-env-configuration
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki
source_ref: wiki:8d4a2d70-a1c6-445a-9d57-d3882007e97e
tags: []
---

# GPPC OP环境配置(Dgpay与gppc-jaywan API)

本页汇总 GPPC OP 在 SIM/UAT/PROD 三套环境下的 Dgpay 配置（费用收款商户号、集成网关 URL、产品号）以及 gppc-jaywan 对外暴露给机构的 API 地址清单。

## Dgpay 配置

### Fee Collection Merchant（Jaywan Fee Collection - Jaywan）

| 环境 | 商户号 |
|---|---|
| SIM | 200000433440 |
| UAT | 200000083365 |
| PROD | 200024937979 |

### New Account

- gppc-OP-Funds Flow

### Dgpay Integration 网关地址

- SIM/TEST：`https://testmbankprepaid.dgpays.com/NetaIntegrationGateway/api/AstraTechIntegrationService/{{METHOD_NAME}}`
- UAT：`https://kongapi.mbankuae-uat.local:8443/uat/api/AstraTechIntegrationService/{{METHOD_NAME}}`
- PROD：（原文未列出）

### Product 配置

| Item | SIM | UAT | PROD |
|---|---|---|---|
| ProductNumber | 051 | 051 | 051 |
| SubProductNumber | 051 | 051 | 051 |

## gppc-jaywan 机构对外 API

### URL 前缀

| 环境 | Url Prefix |
|---|---|
| SIM | `https://sim-gppc-ext.test2pay.com/gppc-jaywan/api/dgpay/{UrlSuffix}` |
| UAT | `https://uat-gppc-ext.test2pay.com/gppc-jaywan/api/dgpay/{UrlSuffix}` |
| PROD | `https://gppc-ext.payby.com/gppc-jaywan/api/dgpay/{UrlSuffix}` |

### API 列表（以 PROD 为例）

| API | Url Suffix | PROD 示例 URL |
|---|---|---|
| Get token | `/get-token` | `https://gppc-ext.payby.com/gppc-jaywan/api/dgpay/get-token` |
| Update prepaid card status | `/update-prepaid-card-status` | `https://gppc-ext.payby.com/gppc-jaywan/api/dgpay/update-prepaid-card-status` |
| Provision | `/provision` | `https://gppc-ext.payby.com/gppc-jaywan/api/dgpay/provision` |
| Balance inquiry | `/balance-inquiry` | `https://gppc-ext.payby.com/gppc-jaywan/api/dgpay/balance-inquiry` |
| Reversal | `/reversal` | `https://gppc-ext.payby.com/gppc-jaywan/api/dgpay/reversal` |
| Declined transaction | `/declined-transaction` | `https://gppc-ext.payby.com/gppc-jaywan/api/dgpay/declined-transaction` |
| Notify courier process | `/notify-courier-process` | `https://gppc-ext.payby.com/gppc-jaywan/api/dgpay/notify-courier-process` |

> SIM/UAT 环境下，将上述 Url Suffix 拼接到对应环境的 Url Prefix 即可得到完整地址。
