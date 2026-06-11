---
id: tbl_tradeii_t_pay_order
object_type: Table
name: "tradeii.t_pay_order (支付订单表 / DCC 金额落库)"
aliases: ["t_pay_order", "tradeii.t_pay_order", "支付订单表", "dcc_markup_amount", "dcc_total_amount", "dcc_currency", "dcc_extension"]
domain: online-business
subdomain: acquire
module: DCC
status: active
owner: QA-Team
reviewer: Jizong.Li
last_reviewed_at: 2026-05-20
source_type: testcase
source_ref: "DCC_Via_CKO 01_E2E DB Check (tradeii.t_pay_order DCC fields)"
tags: ["trade", "table", "DCC", "markup"]
related_services: ["svc_tradeii"]
related_logs: ["service:tradeii"]
---

## 用途
支付订单表,**DCC 金额明细的主要落库位置**。Accepted 交易在此存外币金额、汇率与 markup。

## 关键字段(校验点)
- `dcc_total_amount`:用户支付的 DCC 外币总额(含 markup)。
- `dcc_markup_amount`:markup 外币金额。
- `dcc_currency`:DCC 外币币种。
- `dcc_extension`:DCC 扩展(quoteId、exchangeRate 等)。

## 校验要点
- Accepted:上述字段非空且与报价/Get Order/通知一致;交易金额=外币。
- Declined / NotEligible:DCC 字段为空或不作为交易金额。
- 退款:退款外币金额按原汇率/末笔差额计算后,与本表原始 DCC 金额勾稽。

## 常见问题
- markup 金额/币种错落;dcc_extension 缺字段导致对账/账单取数为空。
