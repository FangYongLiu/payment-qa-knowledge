---
id: api_sgs_acquire_revoke_order
object_type: API
name: 收单订单冲正接口(acquire2/revokeOrder)
aliases: [revokeOrder, acquire2_revokeOrder, 冲正]
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-06-25'
source_type: 接口文档
source_ref: PayBy API v2.25 p15
tags: [online-business, acquiring, SGS, 冲正, 退款]
related_services: [svc_sgs, svc_acquireii]
related_tables: [tbl_acquireii_t_acquire_order, tbl_acquireii_t_revoke_order, tbl_acquireii_t_refund_order]
related_scenarios: [scn_online_business_direct_pay]
---

# 收单订单冲正接口(acquire2/revokeOrder)

## 用途
商户认为交易可能失败(发到 PayBy 的收单交易未得到响应、不确定是否成功)时的补救:发起冲正请求。**若 PayBy 端已支付成功则发起退款,否则关闭未支付订单**。

特性:
- **无冲正查询接口**,冲正结果通过 [[api_sgs_acquire_get_order]] 查 `revoked`(true=已冲正)。
- 冲正过程不可查询(如退款进度)。
- 已结算订单状态不再变更,即使被冲正,冲正通过退款订单反映。
- 未支付订单冲正后 `status` 置 `FAILURE`。

## 关联关系
- **所属服务**:[[svc_sgs]] → [[svc_acquireii]](= `related_services`)。
- **读写的表**:[[tbl_acquireii_t_acquire_order]]、[[tbl_acquireii_t_revoke_order]](冲正订单)、已支付转退款时 [[tbl_acquireii_t_refund_order]]。
- **配套接口**:结果查 [[api_sgs_acquire_get_order]];主动退款见 [[api_sgs_acquire_refund_place_order]]。
- **被哪些场景测**:[[scn_online_business_direct_pay]]。

## 路径 / 方法
- 联调:`https://uat.test2pay.com/sgs/api/acquire2/revokeOrder`;生产:`https://api.payby.com/sgs/api/acquire2/revokeOrder`;POST(JSON)。

## 入参
bizContent = OrderIndexRequest:`merchantOrderNo`。公共 Header/Body 见 [[reference_acquire_protocol_and_codes]]。

## 出参
bizBody = RevokeOrderResponse:`acquireOrder`(新增/关注 `revoked`;未支付冲正后 `status=FAILURE`)。

## 错误码
通用码见 [[reference_acquire_protocol_and_codes]]。特有:`62004`(订单不存在)、`62035`(PayBy 订单号不存在)、`62039 REVOKE_FAILURE`(PayBy 内部错误)、`62041 ACQUIRE_ORDER_REFUNDED`(已退款)、`62046 REVOKE_REJECTED`(冲正被拒)。

## 测试校验点(QA)
- 已支付订单冲正:通过退款订单反映,原订单已结算态不变,`revoked=true`。
- 未支付订单冲正:`status=FAILURE`,`revoked=true`。
- 已退款 → 62041;冲正被拒 → 62046;内部错误 → 62039。
- 冲正结果只能经 getOrder 的 `revoked` 判断(无独立查询接口)。
- requestTime 边界、402/403/601 通用路径;仅成功返回 body;`sign` 验签。
