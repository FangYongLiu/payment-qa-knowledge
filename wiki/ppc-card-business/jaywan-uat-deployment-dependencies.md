---
title: Jaywan UAT、部署与依赖
domain: ppc-card-business
kind: wiki_page
slug: jaywan-uat-deployment-dependencies
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_attachment
source_ref: wiki_attachment:e3c2c891-c5e7-47d3-9cfb-05825c9af14a
tags: []
---

# Jaywan UAT、部署与依赖

本页汇总 Jaywan 预付卡（MBank BIN 发起）项目在 UAT、部署阶段所需的依赖项与 Action Points，涵盖合作方就绪、流程签署与产品配置等先决条件。

## 范围定位

本页聚焦上线前的依赖清单与待办事项；功能范围、产品配置、对账与结算等细节请参见相关页面：

- [[jaywan-prepaid-card-brd-overview]]
- [[jaywan-card-integration-scope]]
- [[jaywan-product-matrix-and-setup]]
- [[jaywan-reconciliation-settlement]]

## Dependencies & Action Points

上线前必须完成的依赖与行动项：

- **MBank to enable BIN for Astratech program** — MBank 为 Astratech 项目启用 BIN
- **Dgpays to expose final APIs in pre-prod** — Dgpays 在预生产环境暴露最终 API
- **Settlement process sign off** — 结算流程签署确认（参见 [[jaywan-reconciliation-settlement]]）
- **Courier partner to confirm readiness** — 快递合作方确认就绪（用于实体卡寄送）
- **SLA sign off** — SLA 签署
- **Product setup** — 产品设置完成（参见 [[jaywan-product-matrix-and-setup]]）

## 合作方就绪要点

- **MBank**：作为 BIN Sponsor，负责 BIN 启用与卡管理 API 提供
- **Dgpays**：作为处理合作方，需在 pre-prod 暴露完整 API 集
- **Courier partner**：用于实体 Jaywan 卡的配送，需在上线前确认能力就绪
- **Astratech**：完成产品设置与运营准入流程

## 流程与协议签署

上线前需完成两项关键签署：

- 结算流程（Settlement process）签署：覆盖 T+1 日结算节奏、AED 结算币种、Scheme 清算路径等
- SLA 签署：覆盖文件交付时间（如对账文件 04:00 AM GST 提供）、争议处理时限（如 Astratech 须在同日 2:00 PM GST 前提出对账差异）等服务承诺

## 与其他模块的衔接

- 产品矩阵与 BIN/Program/Plastic 等配置详见 [[jaywan-product-matrix-and-setup]]
- 对账文件与结算机制详见 [[jaywan-reconciliation-settlement]]
- 门户访问与 MIS 报表交付详见 [[jaywan-portal-and-reporting]]
- 业务域定位参见 [[domain_ppc_card_business]]
