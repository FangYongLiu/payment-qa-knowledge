---
title: PayBy收单API总览
domain: payby-acquire-api
kind: wiki_page
slug: payby-acquire-api-overview
status: active
owner: fangyong.liu@astratech.ae
reviewer: UNREVIEWED
source_type: upload
source_ref: api-docs/payby-api-v2.25-p15
tags: []
---

# PayBy收单API总览

本页汇总 PayBy 收单 API 的接口索引及通用约定，便于按场景快速跳转到对应接口详情。

## 接口清单

| 接口 | 路径（path） | 用途 |
| --- | --- | --- |
| [[api_payby_revoke_order]] 订单冲正 | `/sgs/api/acquire2/revokeOrder` | 商户认为可能交易失败时的补救手段，请求取消该笔交易 |
| [[api_payby_get_save_card]] 查询卡信息 | `/sgs/api/acquire2/getSaveCard` | 通过 saved card token 查询卡信息用于展示 |
| [[api_payby_remove_save_card]] 解绑卡 | `/sgs/api/acquire2/removeSaveCard` | 将 saved card token 置为失效，使该 token 无法再被查询和使用 |
| [[api_payby_get_cashier_url_info]] 查询收银台URL信息 | `/sgs/api/acquire2/getCashierUrlInfo` | 返回二维码是否被用户扫描，以及扫码人信息（mask） |

## 环境地址

- 联调（UAT）域名：`https://uat.test2pay.com`
- 生产域名：`https://api.payby.com`
- 完整 URL = 域名 + 上表中对应接口路径。

## 公共请求规范

### Http Header（所有接口一致）

| 字段名 | 变量名 | 必填 | 类型 | 描述 |
| --- | --- | --- | --- | --- |
| 文案语言 | `Content-Language` | Optional | String(10) | en-英文 |
| 签名 | `Sign` | Required | String | |
| 商户号 | `Partner-Id` | Required | String(12) | |

- `Content-Type`: `application/json`

### Http Body 通用结构

- `requestTime`：Timestamp(3)，必填，请求时间（毫秒）。
- `bizContent`：必填，各接口对应的业务内容对象。
  - 冲正：`OrderIndexRequest`
  - 查询卡信息 / 解绑卡：`CardIndexRequest`
  - 查询收银台URL信息：`GetCashierUrlInfoRequest`

## 公共响应规范

- 响应 Header 包含 `Sign`（冲正接口同时回带 `Content-Language`、`Partner-Id`）。
- 响应 Body 由 `head` + `body` 组成：
  - `head`：`ResponseHeader`，必填，包含 `applyStatus`、`code`、`msg`，部分场景还有 `success`、`traceCode`。
  - `body`：可选，仅当 `applyStatus = SUCCESS` 且 `code = 0` 时返回。
- 各接口对应的 body 类型：
  - 冲正 → `RevokeOrderResponse`（含 `acquireOrder`，新增字段 `revoked`）
  - 查询卡信息 → `GetSaveCardResponse`（含 `cardInfo`）
  - 解绑卡 → `Void`
  - 查询收银台URL信息 → `GetCashierUrlInfoResponse`（含 `payer`）

## 通用返回码

以下返回码在 4 个接口中共用：

| code | msg | 含义 |
| --- | --- | --- |
| 0 | SUCCESS | 成功 |
| 400 | INVALID_PARAMETER | 参数错误 |
| 400 | REQUESTTIME_TOO_EARLY | 请求时间比当前时间早太多 |
| 400 | REQUESTTIME_TOO_LATER | 请求时间比当前时间晚太多 |
| 402 | RATE_LIMIT_REJECT | 请求过于频繁 |
| 403 | UNAUTHORIZED | API 未授权 |
| 404 | SERVICE_NOT_AVAILABLE | API 服务不可用 |
| 500 | SYSTEM_ERROR | 系统错误 |
| 504 | SERVICE_TIMEOUT | 服务超时 |
| 601 | RISK_FAIL | 风控校验失败 |

接口专属返回码：

- 冲正：`62004 MERCHANT_ORDER_NO_NOT_EXIST`、`62035 ORDER_NO_NOT_EXIST`、`62039 REVOKE_FAILURE`、`62041 ACQUIRE_ORDER_REFUNDED`、`62046 REVOKE_REJECTED`
- 查询卡信息 / 解绑卡：`62078 CARD_NOT_EXIST`
- 查询收银台URL信息：`62082 TOKEN_URL_NOT_EXIST`

## 冲正业务说明（关键约定）

冲正能力是收单 API 的特殊补救机制，使用前需注意：

- **不提供冲正查询接口**：冲正结果通过查询订单获取，订单上新增冲正标志 `revoked`（`true` 已冲正 / `false` 未冲正）。
- **冲正进度不可见**：商户只能看到 `revoked` 标志，无法查询具体进度（如退款进度）。
- **已结算订单状态不再变更**：即使被冲正，结果通过退款订单反映。
- **未支付订单**：冲正后订单会被置为失败。
- **典型触发场景**：商户发送收单交易后未得到响应，不确定 PayBy 端是否成功；为保护用户利益重新发起冲正——若已成功则发起退款，否则关闭订单。

详见 [[api_payby_revoke_order]]。
