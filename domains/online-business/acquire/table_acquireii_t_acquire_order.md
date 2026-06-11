---
id: tbl_acquireii_t_acquire_order
object_type: Table
name: "acquireii.t_acquire_order (收单订单表)"
aliases: ["t_acquire_order", "acquireii.t_acquire_order", "收单订单表"]
domain: online-business
subdomain: acquire
module: DCC
status: active
owner: QA-Team
reviewer: Sijia.Zhang
last_reviewed_at: 2026-05-20
source_type: testcase
source_ref: "DCC_Via_CKO 01_E2E DB Check (acquireii.t_acquire_order / t_payment_info)"
tags: ["acquire", "table", "DCC"]
related_services: ["svc_acquireii"]
related_logs: ["service:acquireii"]
---

## 用途
收单侧订单登记。下单/资格判定后记录收单订单及其 DCC 决策上下文,是 DB 校验的第一站(配套 `acquireii.t_payment_info`)。

## 关键字段(校验点)
- 订单号、商户、金额/币种、订单状态。
- DCC 决策:`dccUptake`(ACCEPTED/DECLINED/NULL|NOT_APPLICABLE)、关联 `dccQuoteId`。
- 不走 DCC(NotEligible)时不应落 DCC 金额/币种为交易金额。

## 校验要点
- 与 `tbl_tradeii_t_trade_order` / `tbl_tradeii_t_pay_order` 数据一致。
- Accepted:交易币种=外币;Declined/NotEligible:交易币种=AED/商户币种。

## 常见问题
- 资格判定结果与下游落库不一致;NotEligible 误填 DCC 字段。
