---
title: 商户收单错误码速查
domain: merchant-acquisition-testing
kind: wiki_page
slug: merchant-acquisition-error-code-cheatsheet
status: archived
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:AQ/2125922317
tags: []
---

# 商户收单错误码速查

本页汇总商户收单测试中高频出现的错误码与错误信息，按主题分类速查。完整错误码见附录 §A，本页只覆盖**每天都会用到**的部分。错误码出现在接口响应 `head.code`、异步通知 `failCode` 或 `SYSTEM_ERROR(500)` 携带的 `msg` 中，配合 [[merchant-acquisition-e2e-five-stage-verification]] 的段 ① 接口响应一起核对。

## 使用约定

- `head.applyStatus = SUCCESS` ≠ 业务成功；业务结果看 `head.code`。
- `code = 0` 才是业务成功，其余均为业务错误码。
- `500 SYSTEM_ERROR` 通常会带 `traceCode` 和 `msg`，部分场景的细分错误体现在 `msg` 文案中（见下文 Capture/Void/PreAuth）。
- 异步通知的失败原因通过 `failCode` 字段透出（92xxx 段）。

## 全局码

| Code | Message | 含义 |
|---|---|---|
| 0 | SUCCESS | 成功 |
| 400 | INVALID_PARAMETER | 参数错误 |
| 400 | REQUESTTIME_TOO_EARLY/LATER | 时间戳偏差 > 15 分钟 |
| 402 | RATE_LIMIT_REJECT | 限流 |
| 403 | UNAUTHORIZED | 商户无权限（签名错误 / Partner-Id 错误） |
| 500 | SYSTEM_ERROR | 系统错误（一般含 traceCode） |
| 504 | SERVICE_TIMEOUT | 超时 |
| 601 | RISK_FAIL | 风控拦截 |

## 订单状态冲突

跟单据状态机直接相关，常用于幂等、重复请求、状态错配场景。

| Code | Message | 含义 |
|---|---|---|
| 62001 | ORDER_PAID | 订单已付款 |
| 62002 | ORDER_FAILURE | 订单已失败 |
| 62003 | ORDER_SETTLED | 订单已结算 |
| 62004 | MERCHANT_ORDER_NO_NOT_EXIST | 商户订单号不存在 |
| 62015 | ORDER_NOT_PAID | 订单未付款 |
| 62016 | MERCHANT_ORDER_NO_EXIST | 商户订单号已存在（**幂等冲突**） |
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
| 62026 | PRODUCT_IS_NOT_APPLIED | ⭐ 未开通对应产品包 |
| 62065 | INVALID_CARD_NO | 卡号非法 |
| 62078 | CARD_NOT_EXIST | cardToken 不存在或过期 |
| 62079 | MISSING_CARD_NO_CARD_TOKEN | cardNo 和 cardToken 不能都为空 |

> **62026 高频踩坑**：商户 MID 没开通对应产品包时返回，常见于切换 MID 后忘了同步开通产品。

## 风控 / 渠道（异步通知 failCode）

这一段不在同步响应里，而是在 [[merchant-acquisition-notify-statement-spec]] 异步通知 body 的 `failCode` 字段中。

| Code | Message | 含义 |
|---|---|---|
| 92000 | Risk control rejection | 风控拒绝 |
| 92001 | Amount exceeds limit | 金额超限 |
| 92002 | Number of transactions exceeds limit | 交易次数超限 |
| 92003 | Non-KYC user transactions | 用户未实名 |
| 92004 | Channel rejection | 外部通道拒绝 |

## Capture / Void / PreAuth 专属（实测 msg）

注意：以下不是独立的 `code`，而是 `SYSTEM_ERROR(500)` 携带的 `msg` 文案，需要按文案匹配。

| msg | 含义 |
|---|---|
| `SYSTEM_ERROR[Capture amount error]` | Capture 金额超 PreAuth 金额 |
| `SYSTEM_ERROR[Captured order cannot be voided]` | 已 Capture 不能 Void |
| `SYSTEM_ERROR[Capture forbidden, already void]` | 已 Void 不能 Capture |
| `SYSTEM_ERROR[Invalid partner id]` | 跨商户使用资源（cardToken / preauthOrderNo） |
| `PreAuth already voided` | 重复 Void |
| `PreAuth expires` | PreAuth 已过期（默认 7 天） |

## 触发错误码的常用手段

错误码用例属于 [[merchant-acquisition-test-case-skeleton-abcde]] 的 B 组（Negative）和 E 组（Auth & Security）。常用触发方式：

- **B3 外部渠道错误**：用 MPGS 特殊 expiry 触发 —— `05/39 DECLINED` / `04/27 EXPIRED_CARD` / `08/28 TIMED_OUT` / `01/37 ACQUIRER_SYSTEM_ERROR` / `02/37 UNSPECIFIED_FAILURE` / `05/37 UNKNOWN`。详见 [[merchant-acquisition-test-data-preparation]]。
- **B4 风控拒绝**：金额 = 1,000,000 触发限额。
- **B5 幂等冲突**：复用同一 `merchantOrderNo` → `62016`。
- **E1 产品未开通**：换未开通产品包的 MID → `62026 PRODUCT_IS_NOT_APPLIED`。
- **E2 跨商户使用资源**：A 商户的 `cardToken` / `preauthOrderNo` 给 B 商户用 → `Invalid partner id`。
- **E3 签名/Partner-Id 错误**：`403 UNAUTHORIZED`。
- **E4 时间戳偏差**：`requestTime` 偏移 > 15 分钟 → `400 REQUESTTIME_TOO_EARLY/LATER`。
- **E5 IP 白名单**：源 IP 不在配置范围 → 拒绝。

## 排查建议

1. 拿到错误码，先在本页定位类别（全局 / 状态 / 退款 /
