---
id: flow_pix_wechat_mpc_payment
object_type: Flow
name: PIX 微信 MPC 扫码支付端到端流程
aliases: [微信MPC支付, pix-wechat scan-to-pay, STP扫码支付]
domain: channel
status: active
owner: unassigned
reviewer: unassigned
last_reviewed_at: '2026-06-25'
source_type: wiki
source_ref: confluence:PMDPayment/433881954; wiki:a68e3cf4-694f-4d32-9a67-4b4aaeee8675
tags: [pix, wechat, mpc, tenpay, scan-to-pay, 扫码支付]
related_services: []
related_tables: []
related_scenarios: [scn_pix_wechat_vendor_api]
---

# PIX 微信 MPC 扫码支付端到端流程

## 概述
微信 MPC(Merchant Presented Code,商户出示码)扫码支付:境外钱包用户扫描中国大陆商户微信收款码,钱包侧按汇率把交易金额(CNY)换算为支付金额(AED)完成支付,资金最终以 CNY 结算给商户。由 pix-wechat 解析商户码、创建交易、调 Vendor(Tenpay)支付,并处理结果通知、查询、关单与最终支付结果。流程依赖 Rate Sync 同步的汇率与 margin 计费规则。同期有 Alipay(AlipayPlus UPM/MPP)平行接入。
服务对象 svc_pix / svc_pix_wechat 待补(域内尚未建 pix 服务对象)。

## 步骤(跨系统)
### 0. 前置:Rate Sync(汇率同步)
- pix 周期性通过 dubbo api 从 remittance 同步基础汇率(AED→本币),叠加渠道侧 Rate Margin Percent。
- Customer Rate = Exchange Rate × (1 − Margin Percent);Pay Amount = Transaction Amount / Customer Rate。
  - 例:Exchange Rate=1.96688,Margin=0.01 → Customer Rate=1.9472112;200 / 1.9472112 ≈ 102.72。
- 进位规则(Round/Ceiling)与利润口径待补(TODO)。

### 1. Scan and parse code(扫码解析)
- wallet 扫码 → cgs `/pix/mpc/v1/get-rules`(MpcFacade.getMatchRules)→ wallet 本地 match rule。
- wallet → cgs `/pix/mpc/v1/parse`(pix-wechat `MpcFacade.parseCode`):调 Vendor `QUERY_MERCHANT_CODE` 获取商户信息,将商户码信息(含费率)保存到 ES;wallet 展示商户信息。

### 2. Confirm trade information(确认交易信息)
- wallet 根据 rate 计算应付 AED 金额。

### 3. Create trade and pay(创建交易并支付)
- wallet → cgs `/pix/mpc/v1/create-trade`(pix-wechat `MpcFacade.creatTrade`):从 ES 拉商户码信息;调 Vendor `SCAN_CODE_FOR_PAYMENT` 在 vendor 创建交易订单;`CashierTradeFacade#createCashierTrade` 在 tradeii 创建收银台交易并返回 cashierUrl;**按 rate config 校验金额一致**。
- wallet 展示收银台,用户完成 payment process。

### 4. Process trade result(交易结果回调处理)
- Vendor 异步 `NOTIFY_PAYMENT_RESULT`(经 query/tradeii 转交 pix `process result`):
  - 通知 vendor 支付结果(notify payment result);
  - 调 query 保存账单(save bill);
  - 调 reconciliation 保存 fundout glide(save glide);
  - 从 tradeii 取 `instOrderNo`(关键字 `DbtrBankId`)。

### 5. Query trade result(查询交易结果)
- pix 实现 dubbo facade,Vendor `QUERY_PAYMENT_ORDER_INFO` 查本地交易状态。

### 6. Close Payment(关单)
- Vendor `CLOSE_PAYMENT`:pix 收到后调 `TradeOptionalFacade#expireTrade`(tradeii)关闭交易;注意微信关单逻辑。

### 7. Final payment result(最终支付结果)
- Vendor `NOTIFY_FINAL_PAYMENT_RESULT`:若最终支付失败则发起退款([[flow_pix_wechat_refund]]);特别地「最终支付失败但钱包成功」时 pix → tradeii refund 冲销,保持两侧一致。

### 8. wallet 侧状态确认
- wallet → cgs `/pix/mpc/v1/confirm-trade-status` → pix,确认 mpc 订单状态。

## 关联关系
- **经过的服务(有序)**:wallet → cgs → pix(pix-wechat) → vendor(Tenpay) / tradeii / query / reconciliation(服务对象待补)
- **关键表**:ES(商户码信息含费率);tradeii bill、reconciliation glide(对象待补)
- **关键场景 / 参考**:[[scn_pix_wechat_vendor_api]](Vendor API 清单、配置项、字段 Q&A、交易状态机)
- **退款 / 对账**:[[flow_pix_wechat_refund]] / [[flow_pix_wechat_reconciliation]]

## 校验点
- 创建交易时金额需与 rate 配置一致(Check amount with rate config)。
- `TrxDtTm` 日期需与 `TrxId` 日期匹配。
- `NOTIFY_PAYMENT_RESULT` 可能返回失败;trade close / failure 也通过此接口通知。
- `SCAN_CODE_FOR_PAYMENT` 关键字段:`PyerTrxTrmNo`(Device Id)、`BizTp`(来自 QUERY_MERCHANT_CODE)、`ClbckUrl`、`PrmtInf`。
- 最终支付失败需触发退款;「失败但钱包成功」走退款补偿。
- Rate 计费 Round/Ceiling 规则待定(TODO)。

## 交易状态机(Trade Transaction Status)
- P-Processing(入口)→ PS-PaySuccess(收银台支付成功)→ NS-NotifySuccess(成功终态)。
- P-Processing →(trade closed/failed)→ C-Closed(终态);C-Closed →(cashier paid 迟到支付)→ PC-PayCancel。
- PS-PaySuccess →(transaction failed)→ PC-PayCancel。
- 三终态:NS-NotifySuccess(成功)/ C-Closed(关闭)/ PC-PayCancel(撤销)。
- 注:pix SD 设计另有 Trade / Refund 两类状态机,具体字段以原设计图为准(待补:原图未下载)。
