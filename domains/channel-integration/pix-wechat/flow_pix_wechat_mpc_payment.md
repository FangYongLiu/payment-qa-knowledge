---
id: flow_pix_wechat_mpc_payment
object_type: Flow
domain: channel-integration
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-20'
source_type: wiki
source_ref: wiki:a68e3cf4-694f-4d32-9a67-4b4aaeee8675
tags:
- pix
- wechat
- mpc
- payment
subdomain: pix-wechat
module: mpc
sensitivity: normal
name: PIX微信MPC支付端到端流程
aliases: []
related_services: []
related_tables: []
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 概述
PIX 微信 MPC（Merchant Presented Code）支付端到端流程：用户出示微信付款码，商户扫码 → pix-wechat 解析码并获取商户信息 → 钱包按汇率确认 AED 支付金额 → 创建交易并向 vendor 发起支付 → 处理 vendor 异步通知返回的支付结果 → 同步账单与对账资金流。覆盖 Scan and parse code、Create trade and pay、Query trade result、Final payment result 四个核心阶段。

## 步骤(跨系统)

### 1. Scan and parse code（扫码与解析）
- **pix-wechat**：`MpcFacade.parseCode`
  - 调用 vendor API（Requester: `QUERY_MERCHANT_CODE`，路径 `/pix/mpc/v1/parse`）获取商户信息
  - 将商户码信息（含汇率信息）保存到 ES
  - 注意外汇汇率维护由 Remittance Team 负责

### 2. Confirm trade information（钱包确认交易信息）
- **wallet**：根据汇率计算待支付的 AED 金额
  - 计算规则：`Customer Rate = Exchange Rate * (1 - Margin Percent)`，`Pay Amount = Transaction Amount / Customer Rate`

### 3. Create trade and pay（创建交易并支付）
- **pix-wechat**：`MpcFacade.creatTrade`（路径 `/pix/mpc/v1/create-trade`，Requester: `SCAN_CODE_FOR_PAYMENT`）
  - 从 ES 拉取商户码信息
  - 在 vendor 创建交易订单
  - 创建 cashier trade order 并返回 cashierUrl
  - 用汇率配置校验金额

### 4. Process trade result（处理支付结果）
- **pix-wechat**：处理交易订单通知（Requester: `NOTIFY_PAYMENT_RESULT`）
  - 调用 vendor 通知支付结果
  - 调用 query 保存账单
  - 调用 reconciliation 保存 fundout glide
  - 从 tradeii 获取 instOrderNo（关键字 `DbtrBankId`）
- **tradeii / pfs / payment**：保存来自 cmf 的 inst order no，并提供变更 api

### 5. Query trade result（查询交易结果）
- **pix-wechat**：`MpcFacade.parseCode` 实现 dubbo facade 供查询本地交易状态
- 另有 query payment：实现 vendor api 查询本地交易状态

### 6. Final payment result（最终支付结果）
- **pix**：实现 vendor api（Responder: `NOTIFY_FINAL_PAYMENT_RESULT`）
  - 处理最终支付结果
  - 若最终支付失败，则 refund trade

### 7. Other（账单与对账衔接）
- **pix-wechat**：bill synchronization（账单同步）
- **bill**：bill configuration（UI 配置）
- **reconciliation**：reconciliation configuration

## 涉及服务/表
- **服务**：pix-wechat、pix、wallet、tradeii、pfs、payment、bill、reconciliation、remittance、basis-customer
- **存储**：ES（保存商户码信息及汇率信息）
- **Vendor APIs**：
  - `QUERY_MERCHANT_CODE`（Requester） - 解析商户码
  - `SCAN_CODE_FOR_PAYMENT`（Requester） - 创建交易扫码支付
  - `NOTIFY_PAYMENT_RESULT`（Requester） - 处理支付结果通知
  - `QUERY_PAYMENT_ORDER_INFO`（Responder） - 查询支付订单
  - `NOTIFY_FINAL_PAYMENT_RESULT`（Responder） - 通知最终支付结果

## 校验点
- **金额校验**：在 `MpcFacade.creatTrade` 中用汇率配置校验金额（Customer Rate = Exchange Rate * (1 - Margin Percent)）
- **inst order no**：从 tradeii 取 `instOrderNo`，关键字 `DbtrBankId`
- **NOTIFY_PAYMENT_RESULT 失败可能性**：可能收到失败结果（Yes）；可通知 trade close 或 failure（Yes）
- **SCAN_CODE_FOR_PAYMENT 字段**：
  - `PyerTrxTrmNo` = Payer terminal code = Device Id
  - `BizTp` 来自 `QUERY_MERCHANT_CODE`
  - `TrxDtTm` 日期需与 `TrxId` 日期匹配
  - `ClbckUrl`：账户机构回调收单机构 URL
  - `PrmtInf`：营销信息
- **Final payment 失败处理**：若最终支付失败需对交易发起 refund
