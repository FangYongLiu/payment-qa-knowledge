---
id: tbl_tradeii_t_trade_order
object_type: Table
name: "tradeii.t_trade_order (交易订单表)"
aliases: ["t_trade_order", "tradeii.t_trade_order", "交易订单表", "订单表"]
domain: online-business
subdomain: acquire
module: DCC
status: active
owner: QA-Team
reviewer: Jizong.Li
last_reviewed_at: 2026-05-20
source_type: testcase
source_ref: "DCC_Via_CKO 01_E2E DB Check (tradeii.t_trade_order)"
tags: ["trade", "table", "DCC"]
related_services: ["svc_tradeii"]
related_logs: ["service:tradeii"]
---

## 用途
交易订单主表,记录订单状态机与交易币种。tradeii 是主要写入方。

## 关键字段(校验点)
- `order_id`、`status`(CREATED / PAID SUCCESS / SUCCESS / SETTLED)、`update_time`。
- `dccUptake`(ACCEPTED/DECLINED/NULL)、交易币种(Accepted=外币;Declined/NotEligible=AED)。

## 校验要点
- 订单卡处理中:看 `status` 是否停在 PROCESSING、`update_time` 是否长时间不变。
- DCC 金额/汇率/markup 的明细落在 `tbl_tradeii_t_pay_order`,本表存订单级状态与币种。

## 常见问题
- 状态未推进(异步消息丢失);dccUptake 与实际扣款币种不一致。
