---
id: api_sgs_acquire_get_order
object_type: API
name: 收单查询订单接口(acquire2/getOrder)
aliases: [getOrder, acquire2_getOrder]
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-06-25'
source_type: 接口文档
source_ref: PayBy API v2.25 p11
tags: [online-business, acquiring, SGS, 查询, 冲正]
related_services: [svc_sgs, svc_acquireii]
related_tables: [tbl_acquireii_t_acquire_order, tbl_acquireii_t_payment_info]
related_scenarios: [scn_online_business_direct_pay, scn_online_business_mpgs_channel]
---

# 收单查询订单接口(acquire2/getOrder)

## 用途
查询任意 PayBy 收单订单状态,驱动后续业务。适用:① 商户未收到支付通知;② 支付接口返回系统错误/未知状态;③ 关单/撤销前确认状态;④ 查冲正状态(`acquireOrder.revoked=true` 判定冲正成功)。自动化中常用于 `wait_for_order_success` 轮询到终态。

## 关联关系
- **所属服务**:[[svc_sgs]] → [[svc_acquireii]](= `related_services`)。
- **读写的表**:[[tbl_acquireii_t_acquire_order]]、[[tbl_acquireii_t_payment_info]]。
- **被哪些场景测**:[[scn_online_business_direct_pay]]、[[scn_online_business_mpgs_channel]]。
- **配套接口**:撤销前后用本接口确认状态/冲正,见 [[api_sgs_acquire_cancel_order]]、[[api_sgs_acquire_revoke_order]]。

## 路径 / 方法
- 联调:`https://uat.test2pay.com/sgs/api/acquire2/getOrder`;生产:`https://api.payby.com/sgs/api/acquire2/getOrder`;POST(JSON)。

## 入参
bizContent = OrderIndexRequest:`merchantOrderNo`(商户订单号)。公共 Header/Body 见 [[reference_acquire_protocol_and_codes]]。

## 出参
bizBody = GetOrderResponse:`acquireOrder`(AcquireOrder)。关键字段:`status`(如 SETTLED)、`paymentInfo`(paidAmount/paidTime/payChannel 等)、`revoked`、`totalAmount`、`accessoryContent` 等(见 [[reference_acquire_data_models]])。

## 错误码
通用码见 [[reference_acquire_protocol_and_codes]]。特有:`62004 MERCHANT_ORDER_NO_NOT_EXIST`(商户订单号不存在)、`62035 ORDER_NO_NOT_EXIST`(PayBy 订单号不存在)。

## 测试校验点(QA)
- 仅 applyStatus=SUCCESS 且 code=0 返回 body。
- status 覆盖 SETTLED/FAILURE 等典型态;paymentInfo 字段在已支付订单存在且金额/币种正确。
- 冲正判定:`revoked=true`(注意响应字段为 `revoked`)。
- 不存在订单:merchantOrderNo 不存在 → 62004;orderNo 不存在 → 62035。
- requestTime 过早/过晚 → REQUESTTIME_TOO_EARLY/LATER;高频 → 402;未授权 → 403;风控 → 601。
- 响应 Header `sign` 验签。
