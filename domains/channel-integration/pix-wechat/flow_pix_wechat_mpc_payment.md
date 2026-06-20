---
id: flow_pix_wechat_mpc_payment
object_type: Flow
domain: channel-integration
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-20'
source_type: wiki
source_ref: confluence:PMDPayment/433881954
tags:
- MPC
- wechat
- scan-to-pay
subdomain: pix-wechat
module: mpc
sensitivity: normal
name: 微信MPC扫码支付端到端流程
aliases: []
related_services: []
related_tables: []
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 概述
微信MPC(Merchant Presented Code，商户出示码)扫码支付端到端流程：钱包App扫描商户二维码，由 pix-wechat 解析商户码、创建交易、调用Vendor支付，并处理交易结果通知、查询、关单与最终支付结果。流程依赖 Rate Sync 同步的汇率与 margin 计费规则。

## 步骤(跨系统)

### 0. 前置：Rate Sync
- 周期性通过 dubbo api 从 remittance 同步基础汇率(AED→本币)
- pix 配置 Rate Margin Percent
- 计算示例(WECHAT)：Customer Rate = 1.96688000 * (1 - 0.01) = 1.9472112；Pay Amount = 200 / 1.9472112 ≈ 102.72

### 1. Scan and parse code (扫码并解析)
- 系统：pix-wechat
- 入口：`MpcFacade.parseCode`
- 动作：
  - 调用 Vendor API `QUERY_MERCHANT_CODE` 获取商户信息
  - 将商户码信息(含费率信息)保存到 ES
- 参考：pix-SD-MPC

### 2. Confirm trade information (确认交易信息)
- 系统：wallet
- 动作：根据 rate 计算应付 AED 金额

### 3. Create trade and pay (创建交易并支付)
- 系统：pix-wechat
- 入口：`MpcFacade.creatTrade`
- 动作：
  - 从 ES 拉取商户码信息
  - 调 Vendor API `SCAN_CODE_FOR_PAYMENT` 在 vendor 创建交易订单
  - 创建 cashier 交易订单并返回 cashierUrl
  - 校验金额与 rate 配置一致
- 参考：pix-SD-Transaction

### 4. Process trade result (交易结果回调处理)
- 系统：pix-wechat
- Vendor API：Responder `NOTIFY_PAYMENT_RESULT`
- 动作：
  - 处理交易订单通知
  - 调 vendor 通知支付结果
  - 调 query 保存账单
  - 调 reconciliation 保存 fundout glide
  - 从 tradeii 取 `instOrderNo`(关键字 DbtrBankId)
- 关联：tradeii、pfs、payment 保存来自 cmf 的 inst order no 并提供变更API

### 5. Query trade result (查询交易结果)
- 系统：pix-wechat
- Vendor API：Responder `QUERY_PAYMENT_ORDER_INFO`
- 动作：实现 dubbo facade，查询本地交易状态

### 6. Close Payment (关单)
- 系统：pix
- Vendor API：Responder `CLOSE_PAYMENT`
- 动作：实现 vendor api，关闭交易；注意 wechat 关单逻辑

### 7. Final payment result (最终支付结果)
- 系统：pix
- Vendor API：Responder `NOTIFY_FINAL_PAYMENT_RESULT`
- 动作：实现 vendor api；若最终支付失败则发起退款

### 8. Bill / Reconciliation 关联
- pix-wechat：bill synchronization
- bill：bill configuration
- reconciliation：reconciliation configuration

## 涉及服务/表
- 服务：pix-wechat、pix、wallet、remittance、basis-customer、tradeii、pfs、payment、bill、reconciliation
- 存储：ES(商户码信息含费率)
- Vendor API 场景：
  - `QUERY_MERCHANT_CODE` (parse)
  - `SCAN_CODE_FOR_PAYMENT` (create-trade)
  - `NOTIFY_PAYMENT_RESULT` (process trade result)
  - `QUERY_PAYMENT_ORDER_INFO` (query payment)
  - `CLOSE_PAYMENT` (close payment)
  - `NOTIFY_FINAL_PAYMENT_RESULT` (notify final payment result)

## 校验点
- 创建交易时金额需与 rate 配置一致(Check amount with rate config)
- TrxDtTm 日期需与 TrxId 日期匹配
- `NOTIFY_PAYMENT_RESULT` 可能返回失败；可通知 trade close 或 failure
- `SCAN_CODE_FOR_PAYMENT` 关键字段：PyerTrxTrmNo(Device Id)、BizTp(来自 QUERY_MERCHANT_CODE)、ClbckUrl、PrmtInf
- 最终支付失败需触发退款(Refund trade if final payment failed)
- Rate 计费 Round/Ceiling 规则待定(TODO)
