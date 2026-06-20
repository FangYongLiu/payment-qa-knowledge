---
title: Jaywan卡集成功能范围
domain: ppc-card-business
kind: wiki_page
slug: jaywan-card-integration-scope
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_attachment
source_ref: wiki_attachment:e3c2c891-c5e7-47d3-9cfb-05825c9af14a
tags: []
---

# Jaywan卡集成功能范围

本页梳理 Jaywan 预付卡通过 Botim App 发行与管理的集成范围，覆盖虚拟/实体卡发行、Tokenization、3DS、生命周期管理、动态交易权限及 MCC 限制等。整体方案由 MBank 提供 BIN 赞助、Dgpays 作为处理方，Botim 负责钱包余额与最终授权。完整 BRD 背景见 [[jaywan-prepaid-card-brd-overview]]。

## 高阶范围（High Level Scope）

- MBank 提供 BIN 赞助及相关卡管理 API
- 同时支持虚拟卡（Virtual）与实体卡（Physical）
- Botim 管理钱包余额，并发起交易的最终授权（final authorization）
- MBank 通过 SFTP 每日提供 Excel 格式对账文件
- 3DS、Tokenization、交易监控均在集成范围内

## 集成范围明细（Scope of Integration）

- 通过 Botim App 发行虚拟卡与实体卡
- 实体卡配送追踪（Card delivery tracking）
- 面向 Apple Pay 与 Google Pay 的卡 Tokenization
- PIN 创建与更新（PIN creation and update）
- 完整卡生命周期管理：
  - block（冻结）
  - activate（激活）
  - replace（更换）
  - renew（续卡）
  - closure（销卡）
- 动态交易权限：ECOM、POS、ATM
- 基于 MCC 的交易限制（MCC-based transaction restrictions）
- 支持 3DS 的电商交易（3DS-enabled e-commerce）
- 实时余额更新与查询
- 退款（refunds）、冲正（reversals）、拒付（chargeback）及对账工作流

## 交易与卡能力维度

| 维度 | 支持内容 |
| --- | --- |
| 卡形态 | Virtual / Physical |
| 钱包 Token | Apple Pay、Google Pay |
| 交易渠道 | ECOM、POS、ATM（动态启停） |
| 风控限制 | MCC 限制、3DS 校验 |
| 货币 | AED |

## 与其他模块的边界

- 卡设计、BIN 配置、产品类型、PIN 尝试次数、卡有效期等产品参数 → 见 [[jaywan-product-matrix-and-setup]]
- 内部门户操作（卡冻结/激活、Chargeback 提交、报表下载）→ 见 [[jaywan-portal-and-reporting]]
- 每日对账文件、T+1 结算、Advisement 与争议处理 → 见 [[jaywan-reconciliation-settlement]]
- UAT、API 暴露、BIN 启用、SLA 签署等落地依赖 → 见 [[jaywan-uat-deployment-dependencies]]
- 所属业务域：[[domain_ppc_card_business]]
