---
id: scn_online_business_direct_pay
object_type: Scenario
name: 直连支付 (Direct Pay)
aliases: []
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-07-03'
source_type: repo
source_ref: cgs-apitest/testcases/payment/toB/test_direct_pay_fangyong.py (UAT 实跑 2026-07-03)
tags: [online-business, 支付, cgs-apitest, 实测]
related_services: [svc_acquireii, svc_sgs, svc_tradeii, svc_payment, svc_acs, svc_cards, svc_pfs_payment]
related_tables: [tbl_acquireii_t_acquire_order, tbl_acquireii_t_card_info, tbl_tradeii_t_trade_order, tbl_member_tr_bank_account]
related_logs: []
---

# 直连支付 (Direct Pay)

> 业务测试场景。来源 cgs-apitest 回归。穿过 payment-core 交易/支付核心。

## 场景描述
toB 直连支付(DirectPay):商户直接提交卡信息下单,含绑卡/卡token支付、(部分)退款、DCC(动态货币转换)接受/拒绝/退款。链路:sgs/acquireii 下单→tradeii 交易引擎→payment 履约,acs 风控+cards 卡。

## 关联关系
- **涉及服务**:[[svc_acquireii]]、[[svc_sgs]]、[[svc_tradeii]]、[[svc_payment]]、[[svc_acs]]、[[svc_cards]]、[[svc_pfs_payment]](= `related_services`,穿过的服务链)
- **覆盖的自动化**:由覆盖本场景的 AutomationAsset 在其 `related_scenarios` 中声明。
- **读写的表**:[[tbl_acquireii_t_acquire_order]] 收单订单、[[tbl_acquireii_t_card_info]] 卡 token、[[tbl_tradeii_t_trade_order]] 交易单、[[tbl_member_tr_bank_account]] 绑卡。
- 请求样例见 [[reference_acquire_payscene_request_examples]];全链路见 [[flow_cashier_payment]]。

## 实测(UAT 2026-07-03,test_directpay_bindCard)
**请求**:`partnerId=200000080798`、`paySceneCode=DIRECTPAY`、`totalAmount=0.11 AED`、卡 `512345…0009`(MASTERCARD DC)、`riskInfo={scene,level}`;私钥取自 `acs.t_key_config`(CERT_TYPE=PRIVATE)。
**下单响应**:`orderNo=131783076025511093`、`status=CREATED`、`product=Direct Pay`(product_code `200104`),返回 `interActionParams.threeDSecureDom` → 3DS 走 **TEST101** mock 渠道(`.../fundchannelmock/page/3ds/<instNo>/TEST101/VS/<amount>`)。
**mock 3ds + 轮询后查单**:`status=SETTLED`,`paymentInfo`:`payChannel=BANKCARD`、`settlementAmount=0.10`、`payeeFeeAmount=0.01`、`cardInfo.cardToken=…`、`channelParam.AuthCode=…`。
**真实服务链(Kibana,orderNo 追踪,27 服务)**:sgs → [[svc_cashdesk_api]](InitPayInfo/PayOrderFacade)→ [[svc_cmf]] → [[svc_tradeii]](CreateCashierTrade→ConfirmPay)→ [[svc_voucher]] 全局号 → [[svc_acquireii]] → [[svc_payment]] → cmf→[[svc_router]] 选渠道 → tradeii→[[svc_pfs_payment]] 清分 → 扇出([[svc_pns]]/aml/[[svc_statementii]]/[[svc_dpm_accounting]]/deduct/invoice)。

## 落库校验链(实测 SQL → 断言)
| 表 | 关键条件 | 期望 |
| --- | --- | --- |
| [[tbl_acquireii_t_acquire_order]] | `partner_id` + `request_no`(=merchantOrderNo)+ `product_code='200104'` + `pay_scene_code='DIRECTPAY'` | `status='SETTLED'`;`acquire_order_usage='PURCHASE'` |
| [[tbl_tradeii_t_trade_order]] | `partner_id` + `trade_request_no`(=orderNo)+ `trade_amount` | `trade_status='SS'`;`client_id='acquire2'`;`biz_product_code='200104'`;含 `pay_voucher_no`/`settle_voucher_no` |
| [[tbl_member_tr_bank_account]] | `MEMBER_ID` + `OUT_ACCOUNT_TOKEN`(=cardToken) | `STATUS=1`(绑卡有效);`BANK_ID='TESQ'` |
| [[tbl_acquireii_t_card_info]] | `card_token` + `global_id`(=orderNo)+ `card_id` | 存在 1 条;`card_num_maskii='512345******0009'`、`card_level` |

## 校验点(QA)
- 下单返回 status=CREATED + orderNo;命中 3DS 走 threeDSecureDom(TEST101 mock)分支,mock 后 SETTLED。
- **product_code `200104` = Direct Pay**;成功态:acquire_order `SETTLED` + trade_order `SS`。
- 绑卡(saveCard=true):`member.tr_bank_account`(status=1)与 `acquireii.t_card_info`(cardToken)双落;返回 cardToken 供后续 CardToken 支付复用。
- 退款/部分退款金额、状态、settle time;DCC quoteId 无效时 partner rejected(N107)。
- 私钥/公钥取 `acs.t_key_config`(PRIVATE/PUBLIC,enable_flag=Y)。

## 来源与置信
- **UAT 实跑 2026-07-03**(`test_direct_pay_fangyong.py::test_directpay_bindCard`,PASSED):请求/响应/落库为实测;服务链由该订单号 Kibana 追踪(非推断)。
