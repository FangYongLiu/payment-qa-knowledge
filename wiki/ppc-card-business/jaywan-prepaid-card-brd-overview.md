---
title: Jaywan预付卡(MBank)集成BRD总览
domain: ppc-card-business
kind: wiki_page
slug: jaywan-prepaid-card-brd-overview
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_attachment
source_ref: wiki_attachment:e3c2c891-c5e7-47d3-9cfb-05825c9af14a
tags: []
---

# Jaywan预付卡(MBank)集成BRD总览

本页概述 Jaywan 预付卡通过 Botim App 发卡、由 MBank 作为 BIN Sponsor、Dgpays 作为处理方的端到端集成项目目标、范围与利益相关方。详见所属 [[domain_ppc_card_business]]。

## 项目基本信息

- 项目名称：Jaywan Prepaid Card Integration with MBank
- 文档版本：BRD v1.1
- 面向方：MBank – BIN Sponsor Partner

## 项目目标

通过 Botim app 设计并部署端到端的预付卡发卡与管理方案：

- MBank 作为持牌 BIN Sponsor
- Dgpays 作为处理合作方（Processing Partner）
- 面向 Botim 用户提供虚拟卡与实体 Jaywan 卡
- 支持实时余额同步、完整的数字化生命周期管理
- 满足 Scheme 合规交易要求

## 利益相关方

- MBank：提供 BIN Sponsorship 与卡管理 API
- Dgpays：处理方，输出最终 API、提供对账文件
- Astratech / Botim：钱包余额管理、交易最终授权、客服与运营门户使用方
- Jaywan Scheme / CBUAE：清算与结算通道
- Courier Partner：实体卡寄送

## 高层范围 (High Level Scope)

- MBank 提供 BIN Sponsorship 及相关卡管理 API
- 同时支持虚拟卡与实体 Jaywan 卡
- Botim 管理钱包余额并发起交易最终授权
- MBank 通过 SFTP 每日提供 Excel 格式对账文件
- 集成 3DS、Tokenization 与交易监控

## 端到端发卡与管理方案概述

整体方案覆盖以下能力域，详细拆分见各子页：

- 卡发行、生命周期与交易能力 → [[jaywan-card-integration-scope]]
- 内部门户与 MIS 报表 → [[jaywan-portal-and-reporting]]
- 每日 T+1 对账与结算 → [[jaywan-reconciliation-settlement]]
- 产品矩阵、卡设计与产品参数设置 → [[jaywan-product-matrix-and-setup]]
- UAT、部署与依赖项 → [[jaywan-uat-deployment-dependencies]]

## 关键设计原则

- 结算货币：AED
- 时区：所有时间戳使用 UAE GST
- 对账周期：T+1，每日 04:00 AM GST 前交付
- 结算频率：每日，依据前一日对账文件
- 交易需按 Jaywan 要求的 scheme code 分类，确保清算准确性
