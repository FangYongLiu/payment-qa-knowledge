---
id: reference_pix_wechat_mpc_overview
object_type: Reference
name: PIX微信MPC(Merchant Presented Code)渠道接入总览
aliases: [pix-wechat-mpc-overview]
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
source_type: wiki
source_ref: wiki:a68e3cf4-694f-4d32-9a67-4b4aaeee8675
tags: [payment-core, wiki-overview]
related_services: [svc_basis_customer, svc_cmf, svc_payment, svc_pfs_payment, svc_pix, svc_reconciliation, svc_remittance]
related_tables: []
---


# PIX微信MPC(Merchant Presented Code)渠道接入总览

本页汇总 PIX 接入微信 Pay-In-China 商户出示码(MPC)渠道的业务背景、参考资料与整体业务流程框架，作为该渠道接入相关页的入口。

## 业务背景

- 场景：境外钱包用户在中国大陆扫描商户出示的微信收款码完成支付（Merchant Presented Code）。
- 渠道：WECHAT（同期还有 Alipay 平行接入，参见 Vendor APIs 清单）。
- 用户金额换算：钱包侧基于汇率配置把交易金额（CNY）换算为支付金额（AED）。

## 参考文档

- PRD & API：`Pay in China-Wechat`
- Git 文档：`http://gitlab.test2pay.com/pay/doc/doc-payment/-/tree/master/pix/1-Requirement/20240415_wechat_mpc`
- Union Pay PRD：Google Doc `1HRxbhJK-NfWiS7Tlf9FnzCnvFOmcizSROCr1P6QvKX4`
- 业务介绍：`Pay into China - Merchant Presented QR Product Introduction - 29th March.pdf`
- UI（Figma）：`Scan-to-pay` `node-id=60-125`
- AliPay 文档：`docs.alipayplus.com` `product_upm_mpp` `v1.5.2`

## 业务流程概要

商户出示码（Merchant Presented Code）的端到端业务流程见独立流程页：

- [[flow_pix_wechat_mpc_payment]]：扫码解析 → 确认交易信息 → 创建交易并支付 → 查询交易结果 → 处理最终支付结果。
- [[flow_pix_wechat_refund]]：退款（含 10 分钟查询窗口与退款推定 `NOTIFY_PRESUPPTIVE_REFUND_SUCCESS`）。
- [[flow_pix_wechat_reconciliation]]：通过指定 API 下载对账文件并自动对账。

## 系统流程主题分布

整体系统流程拆分为以下主题，详见对应页面：

- 汇率同步与计算规则：见 pix-wechat-rate-sync
  - 基础汇率来源 remittance，按渠道配置 Rate Margin Percent。
- 系统设计（扫码、建单与支付、查询、退款、关单、最终结果、对账等）：见 pix-wechat-system-flow
  - 关键 SD 文档：`pix-SD-MPC`、`pix-SD-Transaction`、`pix-SD-FX Rate`。
- Vendor API 清单与渠道配置：见 pix-wechat-vendor-api-catalog
  - 包括 Requester/Responder 角色划分与 Wechat Configuration 项（PyerAcctIssrId、PyeeAcctIssrId、AppId）。
- 字段说明与 Q&A：见 pix-wechat-qa-notes
  - 涵盖 `SCAN_CODE_FOR_PAYMENT`、`NOTIFY_PAYMENT_RESULT`、`QUERY_PAYMENT_ORDER_INFO`、`REFUND`、`NOTIFY_PRESUPPTIVE_REFUND_SUCCESS` 等 API 的字段含义与常见问题。

## 涉及系统与角色

- pix / pix-wechat：渠道接入主体，承载 MPC 解析、建单、支付结果处理、退款、关单、查询、对账文件下载等。
- wallet：交易信息确认与按汇率换算 AED 支付金额。
- remittance：提供 AED → 本币基础汇率。
- basis-customer：汇率与 margin 的查询/配置 UI。
- bill：账单配置与同步。
- reconciliation：对账配置与自动对账作业。
- tradeii / pfs / payment：保存来自 cmf 的 inst order no（关键字 `DbtrBankId`）并提供变更接口。
