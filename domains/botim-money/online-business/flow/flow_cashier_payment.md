---
id: flow_cashier_payment
object_type: Flow
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-06-24'
source_type: flow_diagram
source_ref: SERVICE_FLOW_CASHIER_PAYMENT.md
tags: [cashier, acquiring, payment, refund]
name: 收银台 / 收单卡支付端到端流程（含退款）
aliases: [收银台支付流程, cashier-payment-flow, 收单卡支付]
related_services: [svc_merchant_frontend, svc_acquireii, svc_voucher, svc_tradeii, svc_ppcenter, svc_cashdesk_api, svc_cashierii, svc_grc_check_identity_provider, svc_grc_cps_provider, svc_member, svc_pbs, svc_cmf, svc_router, svc_pfs_payment, svc_payment, svc_dpm_manager, svc_dpm_accounting, svc_counter, svc_pns, svc_aml, svc_deduct, svc_remittance, svc_host, svc_coupon_service, svc_query_datasync, svc_cgs, svc_authpay]
related_tables: []
---

# 收银台 / 收单卡支付端到端流程（含退款）

> 系统最核心的一条交易链(收银台/收单卡支付)。来源:`SERVICE_FLOW_CASHIER_PAYMENT.md`
> ——cgs-apitest 场景入口 API(代码) × UAT Kibana 观测调用边。候选待人审。

## 正向支付时序（主干）
1. **下单受理**:[[svc_merchant_frontend]] → [[svc_acquireii]](`/acquire2/placeOrder`)
2. **全局号/幂等**:[[svc_acquireii]] → [[svc_voucher]](`getGlobalId`)
3. **创建交易**:[[svc_acquireii]] → [[svc_tradeii]](`createCashierTrade`)
4. **商户产品校验**:[[svc_acquireii]] → [[svc_ppcenter]](`queryMerchantOpenedProductStatus`)
5. **进收银**:[[svc_acquireii]] → [[svc_cashdesk_api]] / [[svc_cashierii]]
   (`cardPayForAnonymous` / `queryPosPayResult`;入口 `/cashdesk/unityInitPayPage`、`/cashierii/*`)
6. **风控**:收银 → [[svc_grc_check_identity_provider]](`riskOtherEvent`,`/risk-identify/*`)
7. **校验支付密码**:[[svc_cashierii]] → [[svc_member]](`checkPassword`)
8. **计费**:[[svc_tradeii]] / 收银 → [[svc_pbs]](`pricingPayFee`)
9. **选渠道**:[[svc_tradeii]] → [[svc_cmf]] → [[svc_router]](`getChannelsByApiTypes`/`queryChannelArchive`)→ 渠道出站
10. **清分**:[[svc_tradeii]] → [[svc_pfs_payment]](`enterMulti`)
11. **记账**:[[svc_payment]] → [[svc_dpm_manager]] / [[svc_counter]]
12. **商户通知**:收银/交易 → [[svc_pns]](`notifyMerchant`)

环路:[[svc_tradeii]] ↔ [[svc_cashierii]] 双向(下单与确认支付结果互调)。

## 退款时序（变体，test_directpay_refund / *_PartialRefund）
[[svc_merchant_frontend]] → [[svc_acquireii]] → [[svc_tradeii]](`queryRefundOrder`/`refund`)→ [[svc_pfs_payment]] 反向清分
→ [[svc_payment]] 记账冲正;查单 `/acquire2/refund/getOrder`。

## 每步证据来源（可溯源）
| 步骤 | 服务边(观测) | 方法(实测) | 入口 API(代码) |
| --- | --- | --- | --- |
| 下单受理 | merchant-frontend→acquireii | — | `/acquire2/placeOrder` |
| 全局号/幂等 | acquireii→voucher | `getGlobalId` | — |
| 创建交易 | acquireii→tradeii | `createCashierTrade` | — |
| 商户产品 | acquireii→ppcenter | `queryMerchantOpenedProductStatus` | — |
| 进收银 | acquireii→cashdesk-api/cashierii | `cardPayForAnonymous`/`queryPosPayResult` | `/cashdesk/unityInitPayPage`,`/cashierii/*` |
| 风控 | 收银→grc | `riskOtherEvent` | `/risk-identify/*` |
| 校验密码 | cashierii→member | `checkPassword` | `/risk-identify/.../check-payment-password` |
| 计费 | tradeii/cashierii→pbs | `pricingPayFee` | — |
| 选渠道 | tradeii→cmf→router | `getChannelsByApiTypes`,`queryChannelArchive` | — |
| 清分 | tradeii→pfs-payment | `enterMulti` | — |
| 记账 | payment→dpm-manager/counter | — | — |
| 通知 | 收银/交易→pns | `notifyMerchant` | — |
| 查单/退款 | acquireii→tradeii | `queryTradeOrder`,`queryRefundOrder`,`refund` | `/acquire2/getOrder`,`/acquire2/refund/*` |

## 真实单笔实测时序（按 paymentOrderNo 从 Kibana 还原 · 非推断）
> 源:`SERVICE_FLOW_REAL_TRACE.md`。单号 `paymentOrderNo=311782162523029632`(唯一,123 条日志/15 服务)。
> 起于**确认支付**(该单号此刻才生成,故下单/收银台初始化段不在此单号内)。

**★ 关键实测结论(修正上面的"理想线性链"理解):**
1. **这是事件驱动(MQ 发布/订阅)流,不是线性 RPC 链**:[[svc_tradeii]] 确认支付后发"支付通知"事件,
   [[svc_aml]](反洗钱上报)/ [[svc_deduct]](代扣)/ [[svc_remittance]] / [[svc_host]](主机记账)/
   [[svc_coupon_service]](优惠券)/ [[svc_query_datasync]](资金同步)等**多个订阅方并行消费**(类名 `*NotifyHandler`/`*Listener`/`*Processor`)。
2. **同步确认支付 ~9 秒内完成**;之后是**异步结算/对账长尾**——[[svc_pfs_payment]] 清分 + [[svc_query_datasync]] 资金操作
   + [[svc_host]] 记账,间隔 3.6min→6.4min→2h→…→**4.8 小时**反复。
3. 同步段关键边(+ms=相对耗时):tradeii ConfirmPayProcessor(+651)→ [[svc_voucher]] 取全局ID(+692)→
   [[svc_cashierii]]→[[svc_grc_cps_provider]] 风控(+744)→ tradeii→[[svc_dpm_accounting]] 记账(+1466)→
   tradeii↔确认(+1745)→ **MQ 扇出**(aml +1848 / remittance +2167 / deduct +2647 / host +6093 / coupon +8780)→
   tradeii→[[svc_pfs_payment]] 发起清分(+2674)→ [[svc_authpay]] 免密验证(+6745)。

**与逻辑重建版的差异(都对,真实版才是这一笔实际时序)**:逻辑版是理想线性链;真实版显示确认支付后是
**事件扇出**(并非顺序调用)+ **异步小时级长尾**。要画下单段需用下单期的 `orderNo/requestNo` 再同样还原。
复现:Kibana `message:"311782162523029632"`,`@timestamp` 升序,全 index。

## 边界
`payment` 的入边、渠道末跳(router→qpay-*→外部)本窗口未直接采到,按职责/概念补。来自单次回归窗口,真实但非穷尽。
MQ 事件边(tradeii→订阅方)是 *ClientImpl 调用图采不到的(异步),靠本单笔 trace 补上。
