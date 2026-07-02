---
id: api_sgs_acquire_cancel_order
object_type: API
name: 收单取消订单接口(acquire2/cancelOrder)
aliases: [cancelOrder, acquire2_cancelOrder]
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-06-25'
source_type: 接口文档
source_ref: PayBy API v2.25 p11
tags: [online-business, acquiring, SGS, 取消订单]
related_services: [svc_sgs, svc_acquireii]
related_tables: [tbl_acquireii_t_acquire_order]
related_scenarios: [scn_online_business_direct_pay]
---

# 收单取消订单接口(acquire2/cancelOrder)

## 用途
撤销**未支付**的 PayBy 收单订单,避免重复支付。典型场景:① 支付失败需换新单号重发,先取消原单;② 用户支付超时,系统退出不再受理。

## 关联关系
- **所属服务**:[[svc_sgs]] → [[svc_acquireii]](= `related_services`)。
- **读写的表**:[[tbl_acquireii_t_acquire_order]]。
- **配套接口**:取消前后用 [[api_sgs_acquire_get_order]] 确认状态与冲正(`revoked`)。
- **被哪些场景测**:[[scn_online_business_direct_pay]]。

## 路径 / 方法
- 联调:`https://uat.test2pay.com/sgs/api/acquire2/cancelOrder`;生产:`https://api.payby.com/sgs/api/acquire2/cancelOrder`;POST(JSON)。

## 入参
bizContent = OrderIndexRequest:`merchantOrderNo`(如 `M172475858661`)。公共 Header/Body 见 [[reference_acquire_protocol_and_codes]]。

## 出参
bizBody = CancelOrderResponse:`acquireOrder`。取消成功后 `status` 变为 `FAILURE`。

## 错误码
通用码见 [[reference_acquire_protocol_and_codes]]。特有:

| code | msg | 触发条件 |
| --- | --- | --- |
| 62001 | ORDER_PAID | 已支付订单不支持撤销 |
| 62002 | ORDER_FAILURE | 已失败订单再次撤销 |
| 62003 | ORDER_SETTLED | 已结算订单撤销 |
| 62004 | MERCHANT_ORDER_NO_NOT_EXIST | 商户订单号不存在 |
| 62035 | ORDER_NO_NOT_EXIST | PayBy 订单号不存在 |

## 测试校验点(QA)
- 状态门禁:已支付 → 62001、已失败 → 62002、已结算 → 62003。
- 取消成功 `head.applyStatus=SUCCESS`、`code=0`,`acquireOrder.status=FAILURE`。
- 订单不存在 → 62004 / 62035;requestTime 边界、402/403/404/500/504/601 通用路径。
- 响应 `sign` 验签;仅成功返回 body。
