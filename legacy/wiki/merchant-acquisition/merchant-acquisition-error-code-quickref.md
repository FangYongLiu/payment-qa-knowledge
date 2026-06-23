---
title: 商户收单高频错误码速查
domain: merchant-acquisition-testing
kind: wiki_page
slug: merchant-acquisition-error-code-quickref
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki
source_ref: wiki:4ef3640b-38b5-4756-81d5-d729c241dc79
tags: []
---

# 商户收单高频错误码速查

本页汇总商户收单测试中每天都会用到的高频错误码，按主题分组速查。完整错误码请见附录 §A；用例分组与触发方式见 [[merchant-acquisition-test-case-skeleton-abcde]]。

## 全局码

| Code | Message | 含义 |
|---|---|---|
| 0 | SUCCESS | 成功 |
| 400 | INVALID_PARAMETER | 参数错误 |
| 400 | REQUESTTIME_TOO_EARLY/LATER | 时间戳偏差 > 15 分钟 |
| 402 | RATE_LIMIT_REJECT | 限流 |
| 403 | UNAUTHORIZED | 商户无权限 |
| 500 | SYSTEM_ERROR | 系统错误（可能含 traceCode） |
| 504 | SERVICE_TIMEOUT | 超时 |
| 601 | RISK_FAIL | 风控拦截 |

> 提示：`applyStatus = SUCCESS` 不代表业务成功，必须看 `head.code`。详见 [[merchant-acquisition-e2e-five-stage-verification]] 段 ①。

## 订单状态冲突

| Code | Message | 含义 |
|---|---|---|
| 62001 | ORDER_PAID | 订单已付款 |
| 62002 | ORDER_FAILURE | 订单已失败 |
| 62003 | ORDER_SETTLED | 订单已结算 |
| 62004 | MERCHANT_ORDER_NO_NOT_EXIST | 商户订单号不存在 |
| 62015 | ORDER_NOT_PAID | 订单未付款 |
| 62016 | MERCHANT_ORDER_NO_EXIST | 商户订单号已存在（幂等冲突） |
| 62035 | ORDER_NO_NOT_EXIST | 系统订单号不存在 |

## 退款 / 撤销

| Code | Message | 含义 |
|---|---|---|
| 62006 | REFUND_AMOUNT_EXCEEDED | 退款超额 |
| 62017 | REFUND_MERCHANT_ORDER_NO_EXIST | 退款单号已存在 |
| 62040 | ACQUIRE_ORDER_REVOKED | 已撤销 |
| 62041 | ACQUIRE_ORDER_REFUNDED | 已退款 |
| 62045 | REFUND_REJECTED | 退款被拒 |
| 62046 | REVOKE_REJECTED | 撤销被拒（如跨日） |

## 卡片 / 产品

| Code | Message | 含义 |
|---|---|---|
| 62012 | PAYSCENECODE_ILLEGAL | paySceneCode 非法 |
| 62026 | PRODUCT_IS_NOT_APPLIED | 未开通对应产品包 ⭐ |
| 62065 | INVALID_CARD_NO | 卡号非法 |
| 62078 | CARD_NOT_EXIST | cardToken 不存在或过期 |
| 62079 | MISSING_CARD_NO_CARD_TOKEN | cardNo 和 cardToken 不能都为空 |

> `62026` 是新接入商户最常见的错误：商户未开通对应产品包。属于 E 组权限用例的核心校验项。

## 风控 / 渠道（异步通知 failCode）

这些 code 出现在异步通知 body 的 `failCode` 字段，而不是同步接口响应。通知重试与回包格式见 [[merchant-acquisition-notify-and-statement]]。

| Code | Message | 含义 |
|---|---|---|
| 92000 | Risk control rejection | 风控拒绝 |
| 92001 | Amount exceeds limit | 金额超限 |
| 92002 | Number of transactions exceeds limit | 交易次数超限 |
| 92003 | Non-KYC user transactions | 用户未实名 |
| 92004 | Channel rejection | 外部通道拒绝 |

## Capture / Void / PreAuth 专属（来自实测）

注：这些不是独立的 code，而是 `SYSTEM_ERROR(500)` 携带的 msg 文本。

| msg | 含义 |
|---|---|
| SYSTEM_ERROR[Capture amount error] | Capture 金额超 PreAuth 金额 |
| SYSTEM_ERROR[Captured order cannot be voided] | 已 Capture 不能 Void |
| SYSTEM_ERROR[Capture forbidden, already void] | 已 Void 不能 Capture |
| SYSTEM_ERROR[Invalid partner id] | 跨商户使用资源 |
| "PreAuth already voided" | 重复 Void |
| "PreAuth expires" | PreAuth 已过期（默认 7 天） |

## 速查使用建议

- 拿到非 0 code，先按主题定位到上面的小节，再去对照场景手册（§5.x）确认是否符合预期。
- `500 SYSTEM_ERROR` 不一定是 bug，先看 msg 文本是不是 PreAuth/Capture/Void 的业务校验。
- 触发错误码时，仍需按 [[merchant-acquisition-per-transaction-checklist]] 验证 DB 落库与 Fund Flow 的"应无记录"预期。
