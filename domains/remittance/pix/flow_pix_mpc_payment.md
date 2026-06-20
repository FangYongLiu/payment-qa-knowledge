---
id: flow_pix_mpc_payment
object_type: Flow
domain: remittance
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-20'
source_type: wiki
source_ref: wiki:f244c1d0-438b-46a8-be70-acdc8cfa85b4
tags:
- Pix
- MPC
- 扫码支付
subdomain: pix
module: mpc
sensitivity: normal
name: Pix MPC扫码支付端到端流程
aliases: []
related_services:
- pix
- pix-channel
- wallet
related_tables: []
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 概述
Pix MPC(Merchant Presented Code，商户呈现码)扫码支付的端到端流程，覆盖从钱包扫码、规则匹配、解析二维码、创建交易、支付到结果查询的完整调用链路。涉及 wallet、pix、pix-channel 三个系统的协作。

## 步骤(跨系统)

### 1. scan(扫码阶段)
- **1 scan** (wallet)：钱包获取商户码匹配规则。Wallet 可缓存规则至少 2 天。
  - **1.1 `/pix/mpc/v1/get-rules`** (pix)：获取用于匹配 QrCode 的规则，包含 match rule type：`PREFIX`。
    - **1.1.1.1 `MpcFacade.getMatchRules`** (pix-channel)：实现 dubbo facade。
- **1.2 match rule** (wallet)：使用上一步获取的规则匹配 QrCode。
- **1.3 `/pix/mpc/v1/parse`** (pix)：匹配 QrCode 获取 vendor code；调用 channel 实现以获取商户和交易信息(含费率信息)；向 wallet 返回 code id。
  - **1.3.1.1 `MpcFacade.parseCode`** (pix-channel)：实现 dubbo facade。
- **1.4 show trade information** (wallet)：展示商户与交易信息。

### 2. confirm trade information(确认交易信息)
- **2 confirm trade information** (wallet)：(可选)输入支付金额；(可选)按汇率计算本地币种金额。
  - **2.1 `/pix/mpc/v1/create-trade`** (pix)：(可选)创建交易；返回 `cashierToken`；按汇率配置校验金额。
    - **2.1.1.1 `MpcFacade.parseCode`** (pix-channel)：实现 dubbo facade。

### 3. payment process(支付处理)
- **3 payment process** (wallet)：复用已有的 cashier 支付流程。

### 4. show trade result(展示结果)
- **4 show trade result** (wallet)：支付成功后(cashier 结果页)，跳转至 MPC 结果页。
  - **4.1 `/pix/mpc/v1/query-trade`** (pix)：查询交易信息。
    - **4.1.1.1 `MpcFacade.parseCode`** (pix-channel)：实现 dubbo facade。

### 其他配套
- **bill**：账单配置(Owner: Yongxin Cao)。
- **reconciliation**：对账配置(Owner: Yibin Xia)。

## 涉及服务/表
- **wallet**：扫码、规则匹配、信息展示、支付入口、结果展示。
- **pix**：对外 CGS API 提供方，接口包括 `/pix/mpc/v1/get-rules`、`/pix/mpc/v1/parse`、`/pix/mpc/v1/create-trade`、`/pix/mpc/v1/query-trade`。
- **pix-channel**：通过 `MpcFacade`(`getMatchRules`、`parseCode`) dubbo facade 提供 channel 实现。

## 校验点
- 钱包对规则的缓存有效期：至少 2 天。
- 规则匹配类型支持：`PREFIX`。
- `parse` 阶段需返回包含费率(rate)在内的商户与交易信息，并向 wallet 返回 code id。
- `create-trade` 阶段需按汇率配置校验金额，并返回 `cashierToken`。
- 支付成功后须跳转到 MPC 结果页，并通过 `query-trade` 查询交易信息。
