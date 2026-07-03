---
id: api_sgs_acquire_refund_place_order
object_type: API
name: 收单退款下单接口(acquire2/refund/placeOrder)
aliases: [refund placeOrder, refund_place_order, 退款下单]
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-06-25'
source_type: 接口文档
source_ref: PayBy API v2.25 p12 + developers.botim.money/docs/refund (2026-07-03)
tags: [online-business, acquiring, SGS, 退款, 分账退款]
related_services: [svc_sgs, svc_acquireii]
related_tables: [tbl_acquireii_t_refund_order, tbl_acquireii_t_sharing_info]
related_scenarios: [scn_online_business_direct_pay, scn_online_business_merchant_split, scn_online_business_mpgs_channel]
---

# 收单退款下单接口(acquire2/refund/placeOrder)

## 用途
对已支付收单订单发起退款,PayBy 验证成功后按原路退回买家账号。**只能对订单创建后 180 天内的订单退款**(对外开放门户 2026-07 契约;内部 v2.25 曾记为 100 天,以对外门户 [[reference_open_api_developer_portal]] 为准)。支持分账退款(`refundSharingAmount=true` 从分账方退费)。

## 关联关系
- **所属服务**:[[svc_sgs]] → [[svc_acquireii]](= `related_services`)。
- **读写的表**:[[tbl_acquireii_t_refund_order]] 退款订单、[[tbl_acquireii_t_sharing_info]] 分账信息。
- **被哪些场景测**:[[scn_online_business_direct_pay]](全/部分退款)、[[scn_online_business_merchant_split]](分账退款)、[[scn_online_business_mpgs_channel]](MPGS 退款)。
- **配套接口**:退款结果查 [[api_sgs_acquire_refund_get_order]]。数据结构见 [[reference_acquire_data_models]]。

## 路径 / 方法
- 联调:`https://uat.test2pay.com/sgs/api/acquire2/refund/placeOrder`;生产:`https://api.payby.com/sgs/api/acquire2/refund/placeOrder`;POST(JSON)。

## 入参
bizContent = PlaceRefundOrderRequest:

| 参数 | 类型 | 必填 | 说明 |
| --- | --- | --- | --- |
| refundMerchantOrderNo | String(64) | Y | 退款商户订单号 |
| originMerchantOrderNo | String(64) | N | 原订单商户订单号;与 originOrderNo 二选一(不可同空/同有) |
| originOrderNo | String(32) | N | 原 PayBy 订单号 |
| amount | Money | Y | 退款金额 |
| notifyUrl | String(200) | N | 后端回调 |
| operatorName | String(200) | N | 退款操作员 |
| reason | String(64) | N | 退款原因 |
| deviceId / secondaryMerchantId | String | N | 二级商户号有值时 deviceId 必填 |
| refundSharingAmount | Boolean | N | 默认 false;true 从分账方退费(未指定 sharingParamList 时按比例从收款方/分账方/PayBy 手续费账户退) |
| sharingParamList | List<SharingParam> | N | refundSharingAmount=true 时生效(结构见数据模型) |

## 出参
bizBody:`refundOrder`(RefundOrder,含 `feeRefunded` 已退还手续费 / `failCode` / `failDes`)+ `refundSummary`(acquireAmount/remainRefundAmount/sharingRemainRefundInfoList)。

### RefundOrderStatus 状态机
| Status | 说明 |
| --- | --- |
| CREATED | 已创建 |
| REFUNDED_SETTLED | 退结算 |
| SUCCESS | 退款成功 |
| FAILURE | 退款失败 |

## 错误码
通用码见 [[reference_acquire_protocol_and_codes]]。特有:`62002 ORDER_FAILURE`、`62004 MERCHANT_ORDER_NO_NOT_EXIST`、`62006 REFUND_AMOUNT_EXCEEDED`(退款额>可退额)、`62015 ORDER_NOT_PAID`(未支付订单退款)、`62017 REFUND_MERCHANT_ORDER_NO_EXIST`(同退款单号不同参数)、`62035 ORDER_NO_NOT_EXIST`、`62040 ACQUIRE_ORDER_REVOKED`(原订单已撤销,不可退)。

## 测试校验点(QA)
- origin 二选一互斥;退款额 > 可退额 → 62006;未支付订单退款 → 62015。
- 全额/部分退款金额、状态流转(CREATED→SUCCESS);落库 [[tbl_acquireii_t_refund_order]]。
- 分账退款 refundSharingAmount=true:sharingParamList 各项与原分账勾稽;Money 币种一致。
- refundSummary:`acquireAmount - 已退总额 = remainRefundAmount`。
