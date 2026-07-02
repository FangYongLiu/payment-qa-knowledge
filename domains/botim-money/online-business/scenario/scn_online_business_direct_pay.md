---
id: scn_online_business_direct_pay
object_type: Scenario
name: 直连支付 (Direct Pay)
aliases: []
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-06-24'
source_type: repo
source_ref: cgs-apitest/testcases/payment
tags: [online-business, 支付, cgs-apitest]
related_services: [svc_acquireii, svc_sgs, svc_tradeii, svc_payment, svc_acs, svc_cards, svc_pfs_payment]
related_tables: []
related_logs: []
---

# 直连支付 (Direct Pay)

> 业务测试场景。来源 cgs-apitest 回归。穿过 payment-core 交易/支付核心。

## 场景描述
toB 直连支付(DirectPay):商户直接提交卡信息下单,含绑卡/卡token支付、(部分)退款、DCC(动态货币转换)接受/拒绝/退款。链路:sgs/acquireii 下单→tradeii 交易引擎→payment 履约,acs 风控+cards 卡。

## 关联关系
- **涉及服务**:[[svc_acquireii]]、[[svc_sgs]]、[[svc_tradeii]]、[[svc_payment]]、[[svc_acs]]、[[svc_cards]]、[[svc_pfs_payment]](= `related_services`,穿过的服务链)
- **覆盖的自动化**:由覆盖本场景的 AutomationAsset 在其 `related_scenarios` 中声明。
- **读写的表**:待补

## 校验点(QA)
- 下单返回 status=CREATED + orderNo;命中 3DS 时走 threeDSecureDom 分支。
- 退款/部分退款金额、状态、settle time;DCC quoteId 无效时 partner rejected(N107)。
- 落库:交易/退款单状态;acs `t_key_config` 渠道私钥。

## 来源与置信
- cgs-apitest payment 套件整理;服务链由调用线索+callgraph 推断,部分标待补。
