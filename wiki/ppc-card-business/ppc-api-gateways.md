---
title: PPC API网关配置
domain: ppc-card-business
kind: wiki_page
slug: ppc-api-gateways
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:AQ/2133098640
tags: []
---

# PPC API网关配置

PPC 对外暴露两个 API 网关，分别承载 App 端调用与内部服务调用，接口文档由 Smart-doc 自动生成。

## 网关一览

| 网关 | 用途 | App / 服务 |
|---|---|---|
| **CGS** (Client Gateway Service) | App / Web / H5 调用 | `gp024_cgs` |
| **SGS** (Server Gateway Service) | 内部服务 / 商户调用 | `gp028_sgs` |

## 接口文档

- 实时 API 文档（Smart-doc 自动生成）：<https://sim-admin.corp.test2pay.com/api-doc/>
- 接口变更 PR 时需同步更新文档与本页。

## 关联清单

- [[ppc-api-inventory-overview]]：PPC API 清单总览与维护信息
- [[ppc-api-card-management]]：经 CGS 暴露的卡管理类 API
- [[ppc-api-transaction]]：经 CGS 暴露的交易/账务类 API
- [[ppc-api-card-network-inbound]]：卡组织/物流回调（入向）API
- [[ppc-api-error-codes]]：通用错误码
- [[ppc-api-test-case-generation-hints]]：基于网关与 API 覆盖的用例生成指引
