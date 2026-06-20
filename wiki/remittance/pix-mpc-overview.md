---
title: PIX MPC 商户呈现码支付总览
domain: remittance
kind: wiki_page
slug: pix-mpc-overview
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:PMDPayment/517832723
tags: []
---

# PIX MPC 商户呈现码支付总览

PIX MPC（Merchant Presented Code，商户呈现码）是 PIX 场景下由商户出示二维码、由用户扫码完成的支付方式，整体流程由 wallet、pix、pix-channel 三方协作完成。

## 术语

| Data | Description |
| --- | --- |
| MPC | Merchant Presented Code（商户呈现码） |

## 参与系统与职责

- **wallet**（App Team）：客户端入口，负责扫码、规则匹配、展示商户与交易信息、收银台支付、展示支付结果。
- **pix**（CGS）：对外提供 MPC 相关 HTTP 接口，包含规则下发、二维码解析、交易创建、交易查询。
- **pix-channel**（Business Developer）：实现 dubbo facade `MpcFacade`，对接具体渠道，提供匹配规则、解析、创建交易、查询交易等能力。
- 其他配套：bill（账单配置）、reconciliation（对账配置）。

## 端到端关键节点

完整时序参见 [[flow_pix_mpc_payment]]。主要分为四个阶段：

### 1. 扫码与解析
- wallet 通过 [[api_pix_mpc_get_rules]] 获取商户码匹配规则；规则可在 wallet 侧缓存至少 2 天。
- 当前支持的匹配规则类型：`PREFIX`。
- wallet 用规则匹配扫到的 QrCode，命中后调用 [[api_pix_mpc_parse]] 解析二维码：
  - 由 pix 调用渠道实现匹配 vendor code，获取商户与交易信息（含费率信息）。
  - 返回 code id 给 wallet。
- wallet 展示商户与交易信息。

### 2. 确认交易信息
- wallet 端可选地让用户输入支付金额。
- wallet 端可选地按 rate 计算本币支付金额。
- 调用 [[api_pix_mpc_create_trade]] 创建交易：
  - 可选创建 trade，返回 `cashierToken`。
  - pix 侧会按 rate 配置校验金额。

### 3. 支付过程
- 走 wallet 已有的 cashier 收银台支付流程。

### 4. 展示交易结果
- 收银台支付成功后，wallet 跳转到 MPC 结果页。
- 调用 [[api_pix_mpc_query_trade]] 查询交易信息并展示。

## Dubbo Facade

pix-channel 通过实现 `MpcFacade` 提供能力，主要方法：

- `MpcFacade.getMatchRules`：被 `/pix/mpc/v1/get-rules` 调用。
- `MpcFacade.parseCode`：被 `/pix/mpc/v1/parse`、`/pix/mpc/v1/create-trade`、`/pix/mpc/v1/query-trade` 调用（均落到该 facade 实现）。

## 配套配置

- **bill**：账单配置（Owner: Yongxin Cao）。
- **reconciliation**：对账配置（Owner: Yibin Xia）。
