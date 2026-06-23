---
title: 微信渠道接入配置项
domain: channel-integration
kind: wiki_page
slug: pix-wechat-configuration
status: archived
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:PMDPayment/433881954
tags: []
---

# 微信渠道接入配置项

本页汇总微信 MPC 渠道接入所需的关键配置项，覆盖 UAT 与 PROD 两套环境。具体取值由对接方在部署时填入，本页仅说明配置项的字段含义与适用范围。

## 配置项清单

下列配置项需分别在 UAT 与 PROD 环境中维护：

| Item | UAT Value | PROD Value |
| --- | --- | --- |
| Account institution identifier / `PyerAcctIssrId` | — | — |
| Acquirer institution identifier / `PyeeAcctIssrId` | — | — |
| Mobile application identifier / `AppId` | — | — |

## 字段说明

- **PyerAcctIssrId**：Account institution identifier，付款方账户机构标识。
- **PyeeAcctIssrId**：Acquirer institution identifier，收单机构标识。
- **AppId**：Mobile application identifier，移动应用标识。

## 相关说明

- 微信渠道汇率与计费配置见 [[pix-wechat-rate-sync]]。
- 配置项在各 Vendor API 中的使用场景见 [[pix-wechat-vendor-api-catalog]]。
- 字段层面更细的取值口径与常见疑问见 [[pix-wechat-qa-notes]]。
- 端到端业务背景见 [[pix-wechat-mpc-integration-overview]]。
