---
id: api_sgs_acquire_place_order
object_type: API
name: 收单创建订单接口(acquire2/placeOrder)
aliases: [placeOrder, acquire2_placeOrder]
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-06-25'
source_type: 接口文档
source_ref: PayBy API v2.25 p9
tags: [online-business, acquiring, SGS, 下单, 幂等]
related_services: [svc_sgs, svc_acquireii]
related_tables: [tbl_acquireii_t_acquire_order, tbl_acquireii_t_pay_scene_param, tbl_acquireii_t_sharing_info, tbl_acquireii_t_promotion_info]
related_scenarios: [scn_online_business_direct_pay, scn_online_business_cashier_pay, scn_online_business_pre_auth, scn_online_business_mpgs_channel]
---

# 收单创建订单接口(acquire2/placeOrder)

## 用途
商户先调本接口在 PayBy 后台生成预支付订单,返回 Token(订单会话标识)后再调起支付。所有 SGS 收单场景(DIRECTPAY/PAYPAGE/DYNQR/QRPAY/AUTODEBIT 等)的统一下单入口。
**幂等**:相同请求重复多次返回当前订单状态;幂等请求不校验请求时间,请求时间以第一次为准。

## 关联关系
- **所属服务**:[[svc_sgs]] 接入网关 → [[svc_acquireii]] 收单核心(= `related_services`)。
- **读写的表**:[[tbl_acquireii_t_acquire_order]] 订单主表、[[tbl_acquireii_t_pay_scene_param]]、[[tbl_acquireii_t_sharing_info]]、[[tbl_acquireii_t_promotion_info]]。
- **被哪些场景测**:[[scn_online_business_direct_pay]]、[[scn_online_business_cashier_pay]]、[[scn_online_business_pre_auth]]、[[scn_online_business_mpgs_channel]]。
- **场景参数/枚举**:见 [[reference_acquire_protocol_and_codes]];订单结构见 [[reference_acquire_data_models]]。

## 路径 / 方法
- 联调:`https://uat.test2pay.com/sgs/api/acquire2/placeOrder`
- 生产:`https://api.payby.com/sgs/api/acquire2/placeOrder`
- 方法:POST(JSON)

## 入参
公共 Header/Body 见 [[reference_acquire_protocol_and_codes]]。bizContent = PlaceAcquireOrderRequest:

| 参数 | 类型 | 必填 | 说明 |
| --- | --- | --- | --- |
| merchantOrderNo | String(64) | Y | 商户订单号(唯一,不可复用) |
| subject | String(64) | Y | 商品标题 |
| totalAmount | Money | Y | 订单金额 |
| expiredTime | Timestamp(3) | N | 不超过请求时间 48h,默认 2h |
| payeeMid | String(20) | N | 收款人会员号,默认商户自己 |
| paySceneCode | String(200) | Y | 支付场景码 |
| paySceneParams | String(512) | N | 支付场景参数(随场景而异) |
| notifyUrl | String(200) | N | 后端通知地址 |
| deviceId | String(200) | N | 终端ID;有二级商户号时必填 |
| secondaryMerchantId | String(64) | N | 二级商户号 |
| accessoryContent | AccessoryContent | N | 附属内容 |
| sharingParamList | List<SharingParam> | N | 分账参数;退款时从 payeeMid 账户扣减 |
| promotionInfoList | List<PromotionInfo> | N | 优惠券(appliedRewardId / settleFlag) |
| subjectAr | String(200) | N | 商品标题阿语 |

## 出参
bizBody = PlaceAcquireOrderResponse:`acquireOrder`(AcquireOrder,见 [[reference_acquire_data_models]])+ `interactionParams`(支付参数)。
**仅在订单状态为 CREATED 时**,按不同 paySceneCode 返回不同 interactionParams(如 DIRECTPAY 返回 `threeDSecureDom`/`installmentUrl`,PAYPAGE/JSAPI 返回 `tokenUrl`)。

## 错误码
通用码见 [[reference_acquire_protocol_and_codes]]。接口特有:

| code | msg | 触发条件 |
| --- | --- | --- |
| 62001 | ORDER_PAID | 已支付订单不支持撤销 |
| 62002 | ORDER_FAILURE | 已失败订单再发起创建 |
| 62003 | ORDER_SETTLED | 已结算订单再发起创建 |
| 62008 | EXPIREDTIME_LESS_THAN_REQUESTTIME | 过期时间小于请求时间 |
| 62009 | EXPIREDTIME_TOO_LATER | 过期时间超过请求时间 48h |
| 62012 | PAYSCENECODE_ILLEGAL | 支付场景码非法 |
| 62016 | MERCHANT_ORDER_NO_EXIST | 同订单号不同业务参数重复创建 |
| 62018 / 62019 | PAYERMID_NOT_EXIST / PAYEEMID_NOT_EXIST | 付款方/收款方账号错误 |
| 62020 | PAYERMID_PAYEEMID_ARE_SAME | 付款方与收款方相同 |
| 62026 | PRODUCT_IS_NOT_APPLIED | 产品未申请 |
| 62031/62032/62033 | MISSING_IAP_DEVICE_ID / MISSING_APP_ID / MISSING_AUTHCODE | 对应场景必填缺失 |
| 62034 | INVALID_APP_ID | 无效 appId |

> 原文 62036 起错误码截断,标「待补:原文未提供完整错误码」。

## 测试校验点(QA)
- 幂等:相同 merchantOrderNo + 相同业务参数重复下单返回同一订单;参数不同 → 62016。
- 各 paySceneCode 的 paySceneParams 必填项校验(QRPAY 缺 authCode → 62033 等)。
- expiredTime 边界:小于请求时间 → 62008;超 48h → 62009。
- 仅 CREATED 才返回 interactionParams;落库 [[tbl_acquireii_t_acquire_order]] status=CREATED + orderNo。
- 分账下单 sharingParamList 序号连号;优惠券 settleFlag。
