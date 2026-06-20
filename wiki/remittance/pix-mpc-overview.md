---
title: Pix MPC(商户呈现码)扫码支付总览
domain: remittance
kind: wiki_page
slug: pix-mpc-overview
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki
source_ref: wiki:f244c1d0-438b-46a8-be70-acdc8cfa85b4
tags: []
---

# Pix MPC(商户呈现码)扫码支付总览

本页介绍 Pix MPC 扫码支付的业务概念、术语与端到端各环节中上下游系统的职责划分。

## 业务概念

- **MPC**: Merchant Presented Code，即商户呈现码（商户出示二维码，由用户扫码发起支付）。
- 适用于 Pix 渠道下的商户码扫码场景。

## 数据字典

| Data | Description |
|------|-------------|
| MPC | Merchant Presented Code |

## 上下游系统分工

| 系统 | 职责 |
|------|------|
| wallet | App 端发起扫码、缓存匹配规则、展示商户与交易信息、串联收银台支付流程、跳转结果页 |
| pix | 提供对外 CGS API（get-rules / parse / create-trade / query-trade），负责规则下发、二维码解析、交易创建与查询 |
| pix-channel | 实现 dubbo facade（如 `MpcFacade.getMatchRules`、`MpcFacade.parseCode`），对接渠道侧获取商户、交易、汇率信息 |
| bill | 账单配置 |
| reconciliation | 对账配置 |

## 关键环节与接口

端到端流程详见 [[flow_pix_mpc_payment]]，主要分四步：

### 1. 扫码与解析
- wallet 通过 [[api_pix_mpc_get_rules]] 拉取商户码匹配规则（建议缓存至少 2 天），匹配规则类型包含 `PREFIX`。
- 匹配命中后调用 [[api_pix_mpc_parse]] 解析二维码，获取 vendor code、商户与交易信息（含汇率），并返回 code id。
- 底层由 `pix-channel` 的 `MpcFacade.getMatchRules` / `MpcFacade.parseCode` 实现。

### 2. 确认交易信息
- wallet 展示商户和交易信息。
- 可选：用户输入金额；可选：根据汇率计算本币应付金额。

### 3. 创建交易
- 通过 [[api_pix_mpc_create_trade]]（可选）创建交易，返回 `cashierToken`，并按汇率配置校验金额。

### 4. 支付与结果查询
- wallet 走既有 cashier 收银台支付流程。
- 支付成功后从收银台结果页跳转至 MPC 结果页，并通过 [[api_pix_mpc_query_trade]] 查询最终交易信息。

## 责任人

| 环节 | Owner |
|------|-------|
| wallet 端实现 | App Team |
| pix CGS API | Zhibin Liu |
| pix-channel dubbo facade 实现 | Business Developer |
| bill 配置 | Yongxin Cao |
| reconciliation 配置 | Yibin Xia |
