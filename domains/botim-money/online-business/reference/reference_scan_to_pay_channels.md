---
id: reference_scan_to_pay_channels
object_type: Reference
name: Scan to Pay 各渠道差异(AliPay / UnionPay / WeChat / Aani)+ UnionPay 场景
aliases: [Scan to Pay, 扫码支付渠道差异, UnionPay 支付场景, PIX Scan to Pay]
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-06-25'
source_type: wiki
source_ref: confluence:PMDPayment/537395306 + wiki:dae1b5ba + wiki:3a542dfa
tags: [online-business, acquiring, scan-to-pay, AliPay, UnionPay, WeChat, Aani]
related_services: [svc_acquireii]
---

# Scan to Pay 各渠道差异 + UnionPay 支付场景

> Scan to Pay(扫码支付)场景下 AliPay / UnionPay / WeChat / Aani 四渠道在商户信息展示、折扣、汇率结算、订单字段上的差异;以及 UnionPay 四种支付场景。QA 跨渠道用例设计与对账校验的依据。

## 金额定义(通用)
- **Transaction Amount (TrxAmount)**:商户应收币种(merchant receivable currency),如 CNY。
- **Payment Amount**:PayBy 币种,默认 AED。

## 商户信息展示

| 项 | AliPay | UnionPay | WeChat | Aani |
| --- | --- | --- | --- | --- |
| Merchant Name | ✅ | ✅ | ✅ | — |
| Merchant Address | ✅ | Only City | ✅ | — |
| Merchant Logo | ❌ | ❌ | ❌ | — |
| TipsFee | ❌ | ✅ | ❌ | — |

## 折扣(Merchant Discount)
- **AliPay**:✅(来源 Decode code)。
- **UnionPay**:Discount Payment Amount(来源 Create Trade Order)。
- **WeChat**:Discount Transaction Amount。
- **Aani**:❌ 不支持。

## 汇率(ExchangeRate)计算与结算方

| 渠道 | Allow Margin | Calc | Settle | 说明 |
| --- | --- | --- | --- | --- |
| AliPay | ✅ | By PayBy | By Ali | 在 A+ 汇率基础上加 extra margin fee |
| UnionPay | ✅ | By PayBy | By UPI | 在 Exchange Service 汇率上加 margin;**当 UnionPay 下单金额(换汇后)超过 payment amount 时拒绝该交易** |
| WeChat | ✅ | By PayBy | By PayBy | 汇率由 PayBy 提供 |
| Aani | — | — | — | No Need(无需换汇) |

## 订单字段(Order Code)

| 字段 | AliPay | UnionPay | WeChat |
| --- | --- | --- | --- |
| Description | ✅ | ✅ | ✅ |
| TrxAmount | ✅ | ✅ | ✅ |
| PaymentAmount 来源 | By PayBy | By UPI(Create Trade Order) | By PayBy |

> PIX SD-Transaction 库表(`pix.t_trade_transaction` 等)的 ER 与字段已在 payment-core 域的 `tbl_pix_*` 与 payment-core 的 [[svc_pix]] 维护,本页不重复。

## UnionPay 四种支付场景

| 场景 | 触发方 | 用户操作入口 | 扣款方式 |
| --- | --- | --- | --- |
| HCE 刷卡 | 用户手机 → POS | Android NFC 刷卡(需开 NFC) | `upic 扣款接口`(钱包) |
| 扫付款码 | 商户扫用户 | 出示银联付款码 | `upic 扣款接口`(钱包);UAE 暂不支持,中国可用 |
| 扫商户码 | 用户扫商户 | Botim App 扫码 → 下单页 | 银联支付接口(涉外币与 AED 换算) |
| EC 银行卡 | 商户页面 | 输入卡号+短信验证码 | upic 应用 → 钱包余额扣款 |

### 扫商户码细节(外币场景关键)
- 用户用 Botim App 扫商户二维码 → 下单页(商户信息 + 金额输入框 + Pay 按钮)→ 点 Pay 呼起收银台(展示预估 AED)→ 校验通过 → 调银联支付接口,银联返回真实 AED。
- 外币:输入框为外币,页面展示「约等于 AED」(汇率每日从银联官网同步);**用户流程在收银台展示后即结束,实际扣款 AED 可能与展示偏差,以银联返回真实 AED 为准**。

### EC 模式(银行卡支付)流程
1. 用户输入银联卡号/有效期/CVV;2. 银联要求输入手机号下发短信验证码;3. 校验通过;4. 银联调 upic 应用经钱包余额扣款。

## 关联关系
- **涉及服务**:[[svc_acquireii]] 收单核心(= `related_services`)。渠道路由经 cmf/router/qpay-* 待补对象。
- **场景码**:扫码支付对应 PaySceneCode `DYNQR`/`QRPAY`,枚举见 [[reference_acquire_protocol_and_codes]]。

## QA 关注点
- 跨渠道商户信息/折扣/汇率字段差异断言(尤其 UnionPay Only City、TipsFee)。
- UnionPay 外币扫商户码:收银台展示 AED 与最终扣款 AED 偏差(以银联真实返回为准)。
- UnionPay 换汇后下单金额超 payment amount 的拒绝分支。
- Aani 无汇率/无折扣的简化路径。
