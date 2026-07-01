---
id: api_sgs_acquire_refund_get_order
object_type: API
name: 收单查询退款订单接口(acquire2/refund/getOrder)
aliases: [refund getOrder, refund_get_order, 查询退款订单]
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-06-25'
source_type: 接口文档
source_ref: PayBy API v2.25 p13
tags: [online-business, acquiring, SGS, 退款, 查询, 分账退款]
related_services: [svc_sgs, svc_acquireii]
related_tables: [tbl_acquireii_t_refund_order]
related_scenarios: [scn_online_business_direct_pay, scn_online_business_merchant_split]
---

# 收单查询退款订单接口(acquire2/refund/getOrder)

## 用途
退款申请后查询退款状态及分账退款明细。通过 `refundMerchantOrderNo`(退款商户订单号)或 `orderNo`(PayBy 订单号)查询(二选一)。

## 关联关系
- **所属服务**:[[svc_sgs]] → [[svc_acquireii]](= `related_services`)。
- **读写的表**:[[tbl_acquireii_t_refund_order]]。
- **配套接口**:退款下单 [[api_sgs_acquire_refund_place_order]]。
- **被哪些场景测**:[[scn_online_business_direct_pay]]、[[scn_online_business_merchant_split]]。

## 路径 / 方法
- 联调:`https://uat.test2pay.com/sgs/api/acquire2/refund/getOrder`;生产:`https://api.payby.com/sgs/api/acquire2/refund/getOrder`;POST(JSON)。

## 入参
bizContent = GetRefundOrderRequest:`refundMerchantOrderNo`(String(64),可选)/ `orderNo`(String(32),可选)——**二选一,不可同空也不可同有**。

## 出参
bizBody:`refundOrder`(RefundOrder) + `refundSummary`。
- **RefundOrder**:refundMerchantOrderNo、orderNo、originMerchantOrderNo、status(如 SUCCESS)、amount、feeRefunded、reason、refundSharingAmount、sharingInfoList[](sharingAmount/sharingIdentitySeqId/sharingMemo/sharingMid/sharingSettledAmount)。
- **refundSummary**:acquireAmount(收单金额)、remainRefundAmount(剩余可退)、sharingRemainRefundInfoList[](remainRefundAmount/memeberId)。

## 错误码
通用码见 [[reference_acquire_protocol_and_codes]]。特有:`62007 REFUND_MERCHANT_ORDER_NO_NOT_EXIST`(退款商户订单号不存在)、`62035 ORDER_NO_NOT_EXIST`。

## 测试校验点(QA)
- 互斥校验:两者同空/同有 → 失败;只填一个 → 通过。
- 未知 refundMerchantOrderNo → 62007;未知 orderNo → 62035。
- 分账退款:refundSharingAmount=true 时 sharingInfoList 各项与请求一致。
- 勾稽:`acquireAmount - 已退总额 = remainRefundAmount`;分账剩余 sharingRemainRefundInfoList 与各分账方累计已退勾稽。
- Money 币种一致;仅成功返回 body;`sign` 验签。
