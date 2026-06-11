---
id: api_acquire2_create_order
object_type: API
name: "DirectPay 创建订单接口 (Create Order)"
aliases: ["Create Order", "创建订单", "currencyConversion", "dccUptake", "确认下单"]
domain: online-business
subdomain: acquire
module: DCC
status: active
owner: QA-Team
reviewer: Sijia.Zhang
last_reviewed_at: 2026-05-20
source_type: testcase
source_ref: "DCC_Via_CKO 01_E2E TC05-TC12 (DirectPay create order + rejections)"
tags: ["DirectPay", "DCC", "createOrder", "CKO"]
related_services: ["svc_acquireii", "svc_tradeii", "svc_router"]
related_tables: ["tbl_tradeii_t_trade_order", "tbl_tradeii_t_pay_order", "tbl_acquireii_t_acquire_order"]
related_scenarios: ["scn_dcc_accepted", "scn_dcc_declined"]
related_logs: ["service:acquireii", "service:tradeii", "channel:CKO302"]
related_failures: ["ts_dcc_create_order_rejected"]
---

## 业务目的
DirectPay 模式下,持卡人对报价做 Accept/Decline 后创建订单。请求带 `currencyConversion`(`dccQuoteId`、`dccUptake`、`exchangeRate`、`markUpRate`、`dccCurrency`、`dccAmount`)+ 卡信息或 `cardToken`。

## 关键请求 / 响应字段
- 请求:`dccQuoteId`、`dccUptake=ACCEPTED|DECLINED`、`exchangeRate`、`markUpRate`、`dccCurrency`、`dccAmount`、卡信息/`cardToken`。
- 响应:`orderId`、订单状态(CREATED/PAID SUCCESS/SETTLE)、`currencyConversion` 对象。

## 行为
- `dccUptake=ACCEPTED`:发往渠道的 `request amount=dccAmount`、`request currency=dccCurrency`、`fundprovider=CKO_DCC_PFAC_01`、Router Channel Code=`CKO302`;渠道处理金额=DCC 金额(非原始 AED)。
- `dccUptake=DECLINED`:用商户/订单币种(AED)处理,渠道金额=订单金额;DCC 仅作决策记录,不用于实际扣款。

## 校验/拒绝规则(必测)
- `dccQuoteId` 不属于当前 partnerId → 拒绝(TC09)。
- `dccQuoteId` 与卡不匹配 → 拒绝(TC10)。
- 篡改 `dccCurrency/dccAmount/markUpRate/exchangeRate` 与报价不一致 → 拒绝(TC11)。
- `dccQuoteId` 过期(>15min)→ 拒绝(TC12)。
- 商户未开通 DCC 仍带 currencyConversion → `UNAUTHORIZED`(TC08)。

## DB 校验
- `tbl_tradeii_t_pay_order`:`dcc_markup_amount/dcc_total_amount/dcc_currency/dcc_extension`;`tbl_tradeii_t_trade_order` 状态与 `dccUptake`。

## Kibana 校验
- `service:acquireii` 看校验与路由;`service:tradeii` 看落单;Channel=`CKO302`。
