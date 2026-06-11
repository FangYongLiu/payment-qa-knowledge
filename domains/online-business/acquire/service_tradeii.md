---
id: svc_tradeii
object_type: Service
name: "tradeii (交易服务)"
aliases: ["tradeii", "交易服务", "TradeII"]
domain: online-business
subdomain: acquire
module: DCC
status: active
owner: QA-Team
reviewer: Jizong.Li
last_reviewed_at: 2026-05-20
source_type: testcase
source_ref: "DCC_Via_CKO service owners: TradeII Jizong.Li"
tags: ["trade", "DCC"]
related_services: ["svc_acquireii"]
related_tables: ["tbl_tradeii_t_trade_order", "tbl_tradeii_t_pay_order"]
related_logs: ["service:tradeii"]
---

## 职责
交易侧落单服务:订单创建、状态推进(CREATED→PAID SUCCESS→SETTLED)、支付与退款落库。DCC 金额、汇率、markup 等写入 `t_pay_order`;接收 acquireii 收单结果完成落单。

## 上下游
- 上游:`svc_acquireii`(收单结果)。
- 下游:payment / cmf(支付与清算,模块 5,本切片不展开)。

## 涉及表
- `tbl_tradeii_t_trade_order`(交易订单、状态、dccUptake)
- `tbl_tradeii_t_pay_order`(支付订单:`dcc_markup_amount/dcc_total_amount/dcc_currency/dcc_extension`)
- `tradeii.t_refund_order`(退款单)

## Kibana / 日志
- `service:tradeii` 看状态机推进与落库结果。

## 常见问题
- 异步消息丢失/积压导致订单卡在处理中(status 不推进);DCC 字段未正确落库。
