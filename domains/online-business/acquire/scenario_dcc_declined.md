---
id: scn_dcc_declined
object_type: Scenario
name: "DCC 拒绝 (Declined) 走商户币种"
aliases: ["DCC Declined", "DCC拒绝", "选择商户币种", "uptake DECLINED"]
domain: online-business
subdomain: acquire
module: DCC
status: active
owner: QA-Team
reviewer: Sijia.Zhang
last_reviewed_at: 2026-05-20
source_type: testcase
source_ref: "DCC_Via_CKO 01_E2E TC03/TC07 (PayPage & DirectPay Declined)"
tags: ["DCC", "declined", "negative"]
related_services: ["svc_acquireii", "svc_tradeii"]
related_tables: ["tbl_tradeii_t_trade_order", "tbl_tradeii_t_pay_order"]
related_scenarios: ["scn_dcc_accepted"]
related_logs: ["service:acquireii", "channel:CKO302"]
---

## 前置条件
DCC 资格满足、展示了选择页,但用户选择**商户币种**(拒绝 DCC)。

## 步骤
1. 展示 DCC 选择页 → 选商户币种(AED)。
2. 提交,`dccUptake=DECLINED`;3DS `Checkout1!` → 成功。

## 预期结果
- 用商户/订单币种处理;渠道 `request amount=订单金额`、`currency=AED`,**不**用外币 DCC 金额扣款。
- 若仍携带 DCC 上下文,仅作决策记录,不用于实际扣款。
- 作为普通非 DCC 支付成功。

## DB 校验
- `tbl_tradeii_t_trade_order`:`dccUptake=DECLINED`、实际交易币种=AED;`tbl_tradeii_t_pay_order` 不以 DCC 外币作为交易金额。

## Kibana 校验
- `service:acquireii` 看决策=DECLINED;Channel `CKO302` 出账币种=AED。

## 关联自动化
- `auto_dcc_qualification_suite`
