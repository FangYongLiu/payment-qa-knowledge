---
id: api_acquire2_refund
object_type: API
name: "DCC 退款与取消接口 (refund / cancelOrder)"
aliases: ["refund/placeOrder", "退款", "全额退款", "部分退款", "末笔退款", "acquire2/cancelOrder", "取消订单", "撤销"]
domain: online-business
subdomain: acquire
module: DCC
status: active
owner: QA-Team
reviewer: Jizong.Li
last_reviewed_at: 2026-05-20
source_type: testcase
source_ref: "DCC_Via_CKO 01_E2E TC13-TC16 (full/partial/last refund, cancel)"
tags: ["DCC", "refund", "cancel", "CKO"]
related_services: ["svc_acquireii", "svc_tradeii"]
related_tables: ["tbl_tradeii_t_trade_order", "tbl_tradeii_t_pay_order"]
related_scenarios: ["scn_dcc_accepted"]
related_logs: ["service:acquireii", "service:tradeii", "channel:CKO302"]
---

## 业务目的
对已 SETTLED 的 DCC 订单退款(`refund/placeOrder`,带 `originOrderNo`)或在未支付成功/未结算前取消(`acquire2/cancelOrder`,全额冲正)。退款发往渠道时用**原 dccCurrency** 和按原汇率换算的外币金额,**不**用 AED。

## 退款金额计算(核心,易错)
- **全额退款**:退外币净额 = 原 `DCC FX NetOrderAmount`(= dccTotal − markup)。例:净额 27.23 USD → 退 27.23 USD。
- **非末笔部分退款**:`退款外币 = 退款订单金额(AED) × 原 exchangeRate`,截断 2 位,**用原汇率、不用最新 FX**。例:AED 40/100 → 0.4 × 27.23 = 10.89 USD。
- **末笔退款**:`= 原交易外币净额 − 历史已退外币之和`(不能用"金额×汇率")。例:27.23 − 10.89 = 16.34 USD。
- **取消(全额冲正)**:退 `DCC TotalTransactionAmount`(含 markup)。例:净额 27.23 + markup 3 = 30.23 USD 全退。

## DB 校验
- `acquireii.t_refund_order`、`tradeii.t_refund_order`、`tradeii.t_pay_order`、`cmf.tt_cmf_order/tt_inst_order/tt_inst_order_result`。
- 退款单关联原 orderNo;退款币种=原 dccCurrency;汇率=原 exchangeRate。

## 结算/资金流
- 系统内部结算仍按 AED;退款手续费按比例,如 charge fee 2.45 × 40/100 = 0.98 AED。

## 常见风险 / 失败模式
- 末笔退款误用"金额×汇率"导致尾差;退款误用最新汇率;退款误用 AED 发渠道。
