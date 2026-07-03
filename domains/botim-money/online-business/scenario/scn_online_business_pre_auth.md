---
id: scn_online_business_pre_auth
object_type: Scenario
name: 预授权 / 请款 (PreAuth-Capture)
aliases: []
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-07-03'
source_type: repo
source_ref: cgs-apitest/testcases/payment/toB/test_pre_auth_capture_fangyong.py (UAT 实跑 2026-07-03)
tags: [online-business, 支付, cgs-apitest, 实测]
related_services: [svc_acquireii, svc_tradeii, svc_payment, svc_cards, svc_acs, svc_preauth, svc_cmf, svc_qpay_mpgs]
related_tables: [tbl_acquireii_t_acquire_order, tbl_acquireii_t_preauth_control, tbl_acquireii_t_preauth_relation, tbl_tradeii_t_trade_order, tbl_cmf_tt_inst_order]
related_logs: []
---

# 预授权 / 请款 (PreAuth-Capture)

> 业务测试场景。来源 cgs-apitest 回归。穿过 payment-core 交易/支付核心。

## 场景描述
toB 预授权-请款:绑卡/卡token(MOTO 带/不带CVV)预授权 → 撤销(Void)/部分请款(Capture)/(部分)退款,含 3DS 降级。

## 关联关系
- **涉及服务**:[[svc_acquireii]]、[[svc_preauth]](预授权订单生命周期)、[[svc_tradeii]]、[[svc_payment]]、[[svc_cards]]、[[svc_acs]]、[[svc_cmf]]/[[svc_qpay_mpgs]](渠道)(= `related_services`)
- **读写的表**:[[tbl_acquireii_t_acquire_order]]、[[tbl_acquireii_t_preauth_control]](授权控制)、[[tbl_acquireii_t_preauth_relation]](请款↔授权关联)、[[tbl_tradeii_t_trade_order]]、[[tbl_cmf_tt_inst_order]](机构订单)。
- 请求样例见 [[reference_acquire_payscene_request_examples]]。

## 实测(UAT 2026-07-03,test_PreAuthCapture_bindCard,商户 200000087655 "MPGS PreAuth Uat")
**product_code = `200111`**(preauth)。两段:
1. **PREAUTH** 授权:下单 CREATED → 3DS(`uat-api.test2pay.com/3ds2/page/...`)→ 查单 `status=AUTHORIZATION`。paymentInfo:`eciValue=02`、`AuthCode/Stan=175498`、`AcquireCode=00 Approved`、`RRN=618411175498`。**授权走渠道 MPGS101**。
2. **CAPTURE** 请款:`paySceneCode=CAPTURE`、`preauthOrderNo=<授权orderNo>` → `status=PAID_SUCCESS`,落 `SETTLED`。**请款走渠道 MPGS132**(与授权 MPGS101 不同)。

**★ 关键实测结论**:预授权与请款走**不同资金渠道**(授权 MPGS101 / 请款 MPGS132);capture 通过 `t_preauth_relation.preauth_order_id` 关联回原授权单,共享 `authorization_id`(如 U51260703069419)。

## 落库校验链(实测)
| 表 | 阶段 | 期望 |
| --- | --- | --- |
| [[tbl_acquireii_t_acquire_order]] | PREAUTH | product `200111` / PREAUTH / `status=AUTHORIZATION` |
| [[tbl_acquireii_t_preauth_control]] | PREAUTH | `authorization_id`、`captured_amount=0`、`capturing_amount=0`、`void_flag=N`、`inst_code=TESQ` |
| [[tbl_acquireii_t_acquire_order]] | CAPTURE | product `200111` / CAPTURE / `status=SETTLED` |
| [[tbl_acquireii_t_preauth_relation]] | CAPTURE | `preauth_order_id`=原授权 global_id、`refunded=N`、同一 `authorization_id` |
| [[tbl_tradeii_t_trade_order]] | CAPTURE | `trade_status=SS`、biz_product `200111`、extension `preauthCapture=Y`/`authorizeRequestNo` |
| [[tbl_cmf_tt_inst_order]] | 各段 | `FUND_CHANNEL_CODE` 授权=MPGS101 / 请款=MPGS132,`STATUS=S` |

## 校验点(QA)
- **状态机**:PREAUTH→AUTHORIZATION;CAPTURE→PAID_SUCCESS/SETTLED;Void(PREAUTHVOID)→释放;部分 Capture / 全额·部分退款。
- **授权 vs 请款走不同渠道**(MPGS101 → MPGS132);capture 关联原授权(preauth_order_id / authorization_id)。
- MOTO CVV/NoCVV 分支;3DS 降级(N108);captured/capturing 金额随请款推进变化。

## 来源与置信
- **UAT 实跑 2026-07-03**(`test_PreAuthCapture_bindCard`,PASSED):请求/响应/落库为实测。
