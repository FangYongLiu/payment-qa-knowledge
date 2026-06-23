---
id: api_payby_refund_get_order
object_type: API
domain: payby-open-api
status: archived
owner: fangyong.liu@astratech.ae
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: upload
source_ref: api-docs/payby-api-v2.25-p13
tags:
- 退款
- 查询
- 分账退款
subdomain: refund
module: null
sensitivity: normal
name: 查询退款订单接口
aliases:
- refund/getOrder
related_services: []
related_tables: []
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
提交退款申请后，通过该接口查询退款状态及分账退款明细。支持通过 `refundMerchantOrderNo`(退款商户订单号) 或 `orderNo`(PayBy订单号) 查询。

## 路径/方法
- 联调URL: `https://uat.test2pay.com/sgs/api/acquire2/refund/getOrder`
- 生产URL: `https://api.payby.com/sgs/api/acquire2/refund/getOrder`
- 方法: HTTP POST，`Content-Type: application/json`

## 入参
### Http Header
| 字段名 | 变量名 | 必填 | 类型 | 描述 |
|---|---|---|---|---|
| 文案语言 | Content-Language | Optional | String(10) | en-英文 |
| 签名 | Sign | Required | String | |
| 商户号 | Partner-Id | Required | String(12) | |

### Http Body
| 字段名 | 变量名 | 必填 | 类型 | 描述 |
|---|---|---|---|---|
| 请求时间 | requestTime | Required | Timestamp(3) | 示例 1581493898000 |
| 业务内容 | bizContent | Required | GetRefundOrderRequest | |

### GetRefundOrderRequest
| 字段名 | 变量名 | 必填 | 类型 | 描述 |
|---|---|---|---|---|
| 退款商户订单号 | refundMerchantOrderNo | Optional | String(64) | refundMerchantOrderNo 和 orderNo 二选一，不能同时为空，且不能同时有值 |
| PayBy订单号 | orderNo | Optional | String(32) | 同上 |

## 出参
### Http Header
- `sign` (Required, String)

### Http Body
- `head`: ResponseHeader (Required)
- `body`: GetRefundOrderResponse (Optional，仅当 `applyStatus=SUCCESS` 且 `code=0` 时返回)

### GetRefundOrderResponse
- `refundOrder`: RefundOrder (Required)

### RefundOrder 关键字段（来自响应样例）
- `refundMerchantOrderNo`: 退款商户订单号
- `orderNo`: PayBy 退款订单号
- `originMerchantOrderNo`: 原始收单商户订单号
- `status`: 退款状态(如 SUCCESS)
- `amount`: Money(currency, amount) 退款金额
- `feeRefunded`: Money 已退手续费
- `reason`: 退款原因
- `reserved`: 保留字段
- `refundSharingAmount`: Boolean 是否退分账金额
- `sharingInfoList[]`: 分账退款明细
  - `sharingAmount`: Money
  - `sharingIdentitySeqId`: Integer
  - `sharingMemo`: String
  - `sharingMid`: String 分账方会员号
  - `sharingSettledAmount`: Money

### refundSummary（响应 body 中同级字段）
- `acquireAmount`: Money 收单金额
- `remainRefundAmount`: Money 剩余可退金额
- `sharingRemainRefundInfoList[]`:
  - `remainRefundAmount`: Money
  - `memeberId`: String 分账方会员号

## 错误码
| code | msg | 原因 | 解决方案 |
|---|---|---|---|
| 0 | SUCCESS | 成功 | |
| 400 | INVALID_PARAMETER | 参数错误 | 调整请求参数 |
| 400 | REQUESTTIME_TOO_EARLY | 请求时间比当前时间早太多 | 调整请求时间 |
| 400 | REQUESTTIME_TOO_LATER | 请求时间比当前时间晚太多 | 调整请求时间 |
| 402 | RATE_LIMIT_REJECT | 请求过于频繁 | 降低请求频率 |
| 403 | UNAUTHORIZED | API未授权 | 联系PayBy |
| 404 | SERVICE_NOT_AVAILABLE | API服务不可用 | 联系PayBy |
| 500 | SYSTEM_ERROR | 系统错误 | 联系PayBy,稍后重试 |
| 504 | SERVICE_TIMEOUT | 服务超时 | 稍后重试 |
| 601 | RISK_FAIL | 风控校验失败 | 请调整业务 |
| 62007 | REFUND_MERCHANT_ORDER_NO_NOT_EXIST | 退款商户订单号不存在 | 修改退款商户订单号 |
| 62035 | ORDER_NO_NOT_EXIST | PayBy订单号的订单不存在 | 调整PayBy订单号 |

## 测试校验点
- `refundMerchantOrderNo` 与 `orderNo` 互斥校验：两者同时为空 → 校验失败；两者同时有值 → 校验失败；只填一个 → 通过。
- Header 必填项缺失校验：缺 `Sign`、`Partner-Id` 应被拒绝。
- `requestTime` 偏移校验：过早返回 `REQUESTTIME_TOO_EARLY`，过晚返回 `REQUESTTIME_TOO_LATER`。
- 不存在订单：用未知 `refundMerchantOrderNo` 期望 `62007`；用未知 `orderNo` 期望 `62035`。
- 成功响应结构：`applyStatus=SUCCESS` 且 `code=0` 时 `body` 返回，否则 `body` 不返回。
- `refundOrder.status` 取值与退款状态机一致(如 SUCCESS 等)。
- 分账退款场景：`refundSharingAmount=true` 时校验 `sharingInfoList` 各项 `sharingAmount`/`sharingSettledAmount`/`sharingMid`/`sharingIdentitySeqId` 与请求一致。
- `refundSummary.acquireAmount`、`remainRefundAmount` 与原单收单金额、累计退款金额勾稽：`acquireAmount - 已退总额 = remainRefundAmount`。
- 分账剩余可退金额：`sharingRemainRefundInfoList[*].remainRefundAmount` 与对应分账方累计已退分账金额勾稽。
- 货币一致性：所有 Money 字段 `currency` 与原单一致(如 AED)。
- 签名校验：响应 Header `sign` 验签通过。
- 频控/未授权/服务不可用等通用错误码路径覆盖(402/403/404/500/504/601)。
