---
id: scn_online_business_cashier_pay
object_type: Scenario
name: 收银台支付 (Cashier / PayPage)
aliases: []
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-07-03'
source_type: repo
source_ref: cgs-apitest/testcases/payment/toB/test_bpg_paypage_fangyong.py (UAT 实跑 2026-07-03)
tags: [online-business, 支付, cgs-apitest, 实测]
related_services: [svc_cashierii, svc_acquireii, svc_tradeii, svc_payment, svc_member, svc_cards, svc_cashdesk_api, svc_pns]
related_tables: [tbl_acquireii_t_acquire_order, tbl_acquireii_t_payment_info, tbl_tradeii_t_trade_order, tbl_pns_t_partner_notify]
related_logs: []
---

# 收银台支付 (Cashier / PayPage)

> 业务测试场景。来源 cgs-apitest 回归。穿过 payment-core 交易/支付核心。

## 场景描述
toB 收银台/受理面支付:BPG PayPage(免登/unauth 收银)、动态二维码、付款码、智慧码、智能POS、出租车、支付链接等多种受理形态。经 cashierii 收银核心 + acquireii 下单 → tradeii/payment。

## 关联关系
- **涉及服务**:[[svc_cashierii]]、[[svc_cashdesk_api]]、[[svc_acquireii]]、[[svc_tradeii]]、[[svc_payment]]、[[svc_member]]、[[svc_cards]]、[[svc_pns]](商户通知)(= `related_services`)
- **读写的表**:[[tbl_acquireii_t_acquire_order]]、[[tbl_acquireii_t_payment_info]](费用/结算)、[[tbl_tradeii_t_trade_order]]、[[tbl_pns_t_partner_notify]](商户异步通知)。

## 实测(UAT 2026-07-03,test_bpg_paypage,商户 200000080798)
**PAYPAGE product_code = `200101`**("Basic Payment Gateway")。下单返回 `interActionParams.tokenUrl`(`uat-checkout.test2pay.com/pay-page/main?BIZ_TYPE=202&ft=<token>`);收银台 `cashdesk/unityInitPayPage` 返回支付方式列表(BALANCE `channelCode=14` / 快捷卡 QUICKPAY `channelCode=15` / GooglePay `channelCode=36` / session_pay 加卡),含 `deductChannel.channelId`、`passwordRequired`、余额 `protocolNo`。查单 `payResult=S` → 落 `SETTLED`。
- N101 匿名卡:pay_channel=BANKCARD;N102 余额:pay_channel=BALANCE(需支付密码)。

**★ 费用/VAT 模型(实测,可直接做断言)**:`t_payment_info` 中
`pf_vat = round(payee_fee_amount × 5.00 / 105.00, 2)`(5% VAT)、`pfbt_amt = payee_fee_amount − pf_vat`、`settlement_amount = paid_amount − payee_fee_amount`、`payer_fee_amount = 0`。例:paid 8.00、payee_fee 0.16 → pf_vat 0.01、pfbt 0.15、settlement 7.84。

## 落库校验链(实测)
| 表 | 关键条件 | 期望 |
| --- | --- | --- |
| [[tbl_acquireii_t_acquire_order]] | product `200101` / PAYPAGE / global_id | `status=SETTLED` |
| [[tbl_acquireii_t_payment_info]] | global_id | `pay_channel`(BANKCARD/BALANCE);费用式:pf_vat/pfbt_amt/settlement_amount 关系成立 |
| [[tbl_tradeii_t_trade_order]] | trade_request_no=orderNo | `trade_status=SS`、biz_product `200101`、control_extension `multiPayer=Y` |
| [[tbl_pns_t_partner_notify]] | VOUCHER_NO=orderNo | event_code ∈ {ACQUIRE_ORDER_PAID, ACQUIRE_ORDER_SUCCESS} 计 ≥1(商户已收异步通知) |

## 校验点(QA)
- 收银台 initTrade→confirmPay→queryResult 全链;免登(unauth)缓存卡/卡token支付/删支付方式。
- 余额/绑新卡/银行卡 多支付方式;退款。
- 各受理形态(POS/QR/智慧码/打车)的下单与回调一致性。

## 来源与置信
- cgs-apitest payment 套件整理;服务链由调用线索+callgraph 推断,部分标待补。
