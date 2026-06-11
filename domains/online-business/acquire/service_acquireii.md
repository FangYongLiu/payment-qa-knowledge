---
id: svc_acquireii
object_type: Service
name: "acquireii (收单服务)"
aliases: ["acquireii", "收单服务", "AcquireII"]
domain: online-business
subdomain: acquire
module: DCC
status: active
owner: QA-Team
reviewer: Sijia.Zhang
last_reviewed_at: 2026-05-20
source_type: testcase
source_ref: "DCC_Via_CKO service owners: AcquireII Sijia.Zhang/Nishil"
tags: ["acquire", "DCC", "CKO"]
related_services: ["svc_tradeii", "svc_router"]
related_tables: ["tbl_acquireii_t_acquire_order", "tbl_tradeii_t_trade_order"]
related_logs: ["service:acquireii"]
---

## 职责
收单侧核心服务:DCC 资格判定、报价编排(调 Metadata/FX)、下单(placeOrder / Create Order)、退款与取消入口。判定是否走 DCC、设 `fundprovider=CKO_DCC_PFAC_01`,把收单结果交给 tradeii 落单。

## DCC 资格判定条件
商户已开通 DCC 产品 + provider=CKO + 卡币种≠AED + 不在黑名单 + Metadata/FX 可用。任一不满足则跳过 DCC 走正常流程。

## 上下游
- 上游:PayPage / DirectPay 入口、商户网关。
- 下游:`svc_router`(路由到 CKO 渠道)、`svc_tradeii`(落单)。

## 涉及 API
- `api_acquire2_place_order`、`api_acquire2_dcc_quotation`、`api_acquire2_create_order`、`api_acquire2_refund`。

## 涉及表
- `tbl_acquireii_t_acquire_order`(收单侧);经 tradeii 间接写 `tbl_tradeii_t_trade_order`、`tbl_tradeii_t_pay_order`。

## Kibana / 日志
- `service:acquireii`;Router Channel Code:Metadata/FX=`CKO123`、支付=`CKO302`。

## 常见问题
- 资格判定缓存/配置不同步;Metadata/FX 失败未正确降级;quoteId 校验(归属/匹配/过期/篡改)。
