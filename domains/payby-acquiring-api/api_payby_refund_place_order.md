---
id: api_payby_refund_place_order
object_type: API
domain: payby-open-api
status: active
owner: fangyong.liu@astratech.ae
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: upload
source_ref: api-docs/payby-api-v2.25-p12
tags:
- refund
- sharing
- acquiring
subdomain: null
module: null
sensitivity: normal
name: 退款下单接口
aliases: []
related_services: []
related_tables: []
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
当订单发生之后一段时间内，由于买家或者卖家原因需要退款时，卖家通过该接口将支付款退还给买家。PayBy 在收到退款请求并验证成功之后，按照退款规则将支付款按原路退到买家账号。只能对 100 天内的订单进行退款。支持分账退款（refundSharingAmount=true 时从分账方退费）。

## 路径/方法
- 联调URL: https://uat.test2pay.com/sgs/api/acquire2/refund/placeOrder
- 生产URL: https://api.payby.com/sgs/api/acquire2/refund/placeOrder
- 方法: HTTP POST，Content-Type: application/json

## 入参
### Http Header
| 字段 | 必填 | 类型 | 说明 |
|---|---|---|---|
| Content-Language | Optional | String(10) | 文案语言，如 en |
| Sign | Required | String | 签名 |
| Partner-Id | Required | String(12) | 商户号 |

### Http Body
| 字段 | 必填 | 类型 | 说明 |
|---|---|---|---|
| requestTime | Required | Timestamp(3) | 请求时间 |
| bizContent | Required | PlaceRefundOrderRequest | 业务内容 |

### PlaceRefundOrderRequest
| 字段 | 必填 | 类型 | 说明 |
|---|---|---|---|
| refundMerchantOrderNo | Required | String(64) | 退款商户订单号 |
| originMerchantOrderNo | Optional | String(64) | 原订单商户订单号；与 originOrderNo 二选一，不能同时为空，也不能同时有值 |
| originOrderNo | Optional | String(32) | 原 PayBy 订单号 |
| amount | Required | Money | 退款金额 |
| notifyUrl | Optional | String(200) | 后端回调地址 |
| operatorName | Optional | String(200) | 退款操作员名称 |
| reason | Optional | String(64) | 退款原因 |
| deviceId | Optional | String(200) | 终端ID；二级商户号有值时必填 |
| secondaryMerchantId | Optional | String(64) | 二级商户号 |
| reserved | Optional | String(20) | 保留字段 |
| refundSharingAmount | Optional | Boolean | 退分账，默认 false；true 表示从分账方退费，未指定 sharingParamList 时按比例从收款方、分账方、PayBy 手续费账户退费 |
| sharingParamList | Optional | List<SharingParam> | 当 refundSharingAmount=true 时生效 |

### SharingParam
| 字段 | 必填 | 类型 | 说明 |
|---|---|---|---|
| sharingAmount | Required | Money | 金额 |
| sharingIdentity | Required | String(200) | 分账方标识；PHONE_NO 需带区号；MEMBER_ID 传 PayBy 会员ID；需加密 |
| sharingIdentitySeqId | Required | Integer | 序号，从 1 开始连号，不可重复 |
| sharingMemo | Required | String(128) | 备注 |
| sharingIdentityType | Required | String(64) | PHONE_NO / MEMBER_ID / TOTOK_UID |
| withholdAndRemitFee | Optional | Boolean | 分账方代收代缴支付手续费；所有分账条目中最多出现一次或不出现，不出现表示无手续费策略 |

## 出参
### Http Header
- sign: Required, String

### Http Body
| 字段 | 必填 | 类型 | 说明 |
|---|---|---|---|
| head | Required | ResponseHeader | 响应头 |
| body | Optional | PlaceRefundOrderResponse | 仅当 applyStatus=SUCCESS 且 code=0 时返回 |

### PlaceRefundOrderResponse
| 字段 | 必填 | 类型 | 说明 |
|---|---|---|---|
| refundOrder | Optional | RefundOrder | 退款订单信息 |
| refundSummary | Optional | RefundSummary | 退款汇总 |

RefundOrder 包含：refundMerchantOrderNo、orderNo、originMerchantOrderNo、status、amount、feeRefunded、reason、reserved、refundSharingAmount、sharingInfoList（含 sharingAmount、sharingIdentitySeqId、sharingMemo、sharingMid、sharingSettledAmount）。

RefundSummary 包含：acquireAmount、remainRefundAmount、sharingRemainRefundInfoList（含 remainRefundAmount、memeberId）。

### RefundOrderStatus 状态机
| Status | 说明 |
|---|---|
| CREATED | 已创建 |
| REFUNDED_SETTLED | 退结算 |
| SUCCESS | 退款成功 |
| FAILURE | 退款失败 |

## 错误码
| code | msg | 原因 | 解决方案 |
|---|---|---|---|
| 0 | SUCCESS | 成功 | - |
| 400 | INVALID_PARAMETER | 参数错误 | 调整请求参数 |
| 400 | REQUESTTIME_TOO_EARLY | 请求时间比当前早太多 | 调整请求时间 |
| 400 | REQUESTTIME_TOO_LATER | 请求时间比当前晚太多 | 调整请求时间 |
| 402 | RATE_LIMIT_REJECT | 请求过于频繁 | 降低请求频率 |
| 403 | UNAUTHORIZED | API 未授权 | 联系 PayBy |
| 404 | SERVICE_NOT_AVAILABLE | API 服务不可用 | 联系 PayBy |
| 500 | SYSTEM_ERROR | 系统错误 | 联系 PayBy 稍后重试 |
| 504 | SERVICE_TIMEOUT | 服务超时 | 稍后重试 |
| 601 | RISK_FAIL | 风控校验失败 | 调整业务 |
| 62002 | ORDER_FAILURE | 已失败的订单发起退款 | 调整商户订单号 |
| 62004 | MERCHANT_ORDER_NO_NOT_EXIST | 商户订单号的订单不存在 | 调整商户订单号 |
| 62006 | REFUND_AMOUNT_EXCEEDED | 退款金额大于可退金额（原金额-已退-退款中） | 调整退款金额 |
| 62015 | ORDER_NOT_PAID | 未支付订单发起退款 | 调整业务 |
| 62017 | REFUND_MERCHANT_ORDER_NO_EXIST | 相同退款订单号但其他业务参数不同 | 调整退款商户订单号 |
| 62035 | ORDER_NO_NOT_EXIST | PayBy 订单号的订单不存在 | 调整 PayBy
