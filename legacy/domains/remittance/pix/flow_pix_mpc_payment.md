---
id: flow_pix_mpc_payment
object_type: Flow
domain: remittance
status: archived
owner: wiki-sync@acquire
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-20'
source_type: wiki
source_ref: confluence:PMDPayment/517832723
tags:
- PIX
- MPC
- 支付流程
subdomain: pix
module: mpc
sensitivity: normal
name: PIX MPC 扫码支付端到端流程
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
PIX MPC (Merchant Presented Code) 商户呈现码扫码支付的端到端流程，涵盖 wallet、pix、pix-channel 三方交互。流程分为四个主阶段：扫码解析、确认交易信息、支付处理、展示交易结果。

## 步骤(跨系统)

### 1 scan(扫码)
- **1 wallet**: Get rules of merchant codes；Wallet 可缓存规则至少 2 天
- **1.1 pix - `/pix/mpc/v1/get-rules`**: 获取用于匹配 QrCode 的规则；包含匹配规则类型：PREFIX
  - **1.1.1.1 pix-channel - `MpcFacade.getMatchRules`**: Implement dubbo facade
- **1.2 wallet - match rule**: 使用上一步获取的规则匹配 QrCode
- **1.3 pix - `/pix/mpc/v1/parse`**: 匹配 QrCode 获取 vendor code；调用 channel 实现获取商户与交易信息(包含费率信息)；返回 code id 给 wallet
  - **1.3.1.1 pix-channel - `MpcFacade.parseCode`**: Implement dubbo facade
- **1.4 wallet - show trade information**: 展示商户与交易信息

### 2 confirm trade information(确认交易信息)
- **2 wallet**: (可选)输入支付金额；(可选)使用费率计算待支付的本币金额
- **2.1 pix - `/pix/mpc/v1/create-trade`**: (可选)创建交易；返回 cashierToken；按费率配置校验金额
  - **2.1.1.1 pix-channel - `MpcFacade.parseCode`**: Implement dubbo facade

### 3 payment process(支付处理)
- **3 wallet**: 走现有的 cashier 收银台支付流程

### 4 show trade result(展示交易结果)
- **4 wallet**: 支付成功(cashier 结果页)后跳转到 MPC 结果页
- **4.1 pix - `/pix/mpc/v1/query-trade`**: 查询交易信息
  - **4.1.1.1 pix-channel - `MpcFacade.parseCode`**: Implement dubbo facade

### 其他
- **bill**: 账单配置 (Owner: Yongxin Cao)
- **reconciliation**: 对账配置 (Owner: Yibin Xia)

## 涉及服务/表
- **wallet** (App Team)：扫码、规则匹配、展示交易信息、收银台支付、结果页跳转
- **pix** (Owner: Zhibin Liu)：CGS API 层，提供 get-rules、parse、create-trade、query-trade 接口
- **pix-channel** (Business Developer)：实现 dubbo facade `MpcFacade`(getMatchRules / parseCode)

## 校验点
- Wallet 对 merchant code rules 的缓存有效期至少 2 天
- 匹配规则类型支持 PREFIX
- `/pix/mpc/v1/parse` 返回必须包含 vendor code、商户与交易信息、费率信息及 code id
- `/pix/mpc/v1/create-trade` 须按费率配置校验金额，并返回 cashierToken
- 支付成功后须从 cashier 结果页跳转到 MPC 结果页，并通过 query-trade 查询确认结果
