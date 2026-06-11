---
id: svc_router
object_type: Service
name: "router (渠道路由服务)"
aliases: ["router", "渠道路由", "Router", "CKO 路由", "qpay-cko"]
domain: online-business
subdomain: acquire
module: DCC
status: active
owner: QA-Team
reviewer: Hefei.Zhang
last_reviewed_at: 2026-05-20
source_type: testcase
source_ref: "DCC_Via_CKO service owners: Router/qpay-cko Hefei.Zhang; Router Channel Codes"
tags: ["router", "CKO", "channel"]
related_services: ["svc_acquireii"]
related_logs: ["channel:CKO123", "channel:CKO302"]
---

## 职责
把收单请求路由到上游渠道 CKO(Checkout.com)。DCC 链路用到的 fundprovider 为 `CKO_DCC_PFAC_01`,并按用途使用不同 Router Channel Code。

## Router Channel Code 约定
- `CKO123`:Get Card **Metadata** API 与 **FX Rate** API(报价阶段)。
- `CKO302`:**支付/清算**出账请求(下单确认后);对账侧 `fund_channel_code=CKO302`。

## 出账请求要点(DCC Accepted)
- `fundprovider=CKO_DCC_PFAC_01`、`sub_entity` 正确、`request amount=dccAmount`、`request currency=dccCurrency`、使用正确商户 key。
- 渠道响应 `acquirerCode=00` 表示成功;渠道处理金额应等于 DCC 金额(非原始 AED)。

## Kibana / 日志
- `channel:CKO123`(metadata/FX)、`channel:CKO302`(支付)。

## 常见问题
- provider≠CKO 时 DCC 不可用;Metadata/FX(CKO123)失败需正确降级;出账金额/币种与用户所选 DCC 不一致。
