---
id: scn_dcc_accepted
object_type: Scenario
name: "DCC 接受 (Accepted) 主路径"
aliases: ["DCC Accepted", "DCC接受", "选择外币", "uptake ACCEPTED"]
domain: online-business
subdomain: acquire
module: DCC
status: active
owner: QA-Team
reviewer: Sijia.Zhang
last_reviewed_at: 2026-05-20
source_type: testcase
source_ref: "DCC_Via_CKO 01_E2E TC01/TC02/TC05/TC06 (PayPage & DirectPay Accepted)"
tags: ["DCC", "happy-path", "accepted"]
related_services: ["svc_acquireii", "svc_tradeii", "svc_router"]
related_tables: ["tbl_tradeii_t_trade_order", "tbl_tradeii_t_pay_order"]
related_scenarios: ["scn_dcc_declined"]
related_logs: ["service:acquireii", "service:tradeii", "channel:CKO302"]
---

## 前置条件
商户开通 DCC、provider=CKO_DCC_PFAC_01、卡币种≠AED 且不在黑名单、Metadata/FX 可用。覆盖 PayPage(新卡/存卡)与 DirectPay(新卡/cardToken)。

## 步骤
1. 报价(quotation 或 placeOrder 后资格判定)→ 展示 DCC 选择页。
2. 选外币(ACCEPTED)→ 提交;请求中 `dccQuoteId/dccCurrency/exchangeRate/markUp` 与 FX 响应严格一致。
3. 3DS 密码 `Checkout1!` → 支付成功。

## 预期结果
- `dccUptake=ACCEPTED`;渠道出账 `amount=dccAmount`、`currency=dccCurrency`、`acquirerCode=00`。
- 渠道处理金额=DCC 外币(非原始 AED)。

## DB 校验
- `tbl_tradeii_t_pay_order`:`dcc_total_amount/dcc_markup_amount/dcc_currency/dcc_extension` 正确;`tbl_tradeii_t_trade_order` 状态 success/settled、交易币种=外币。

## Kibana 校验
- `service:acquireii`(资格/锁汇率)、`service:tradeii`(落单)、Channel `CKO302`。

## 关联自动化
- `auto_dcc_qualification_suite`
