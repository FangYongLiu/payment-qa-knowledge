---
title: CKO订阅支付路由决策机制
domain: channel-integration
kind: wiki_page
slug: cko-subscription-routing-mechanism
status: archived
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:AQ/2228977707
tags: []
---

# CKO订阅支付路由决策机制

本页聚焦 CKO 订阅支付的路由判定逻辑：router 如何依据 `preferSign`、`is3DS` 与签约状态过滤渠道，以及签约支付、代扣订阅在收银台和渠道侧的关键传参与最终渠道映射。业务总览见 [[cko-subscription-payment-overview]]，收银台交互细节见 [[cko-subscription-cashier-flow]]。

## 路由决策三要素

最终渠道由三项联合决定：

```
preferSign 传参 + 用户是否已有签约协议 + 核身项 (is3DS / 密码 / 免密)
                          ⟹ 决定路由渠道
```

- `is3DS=Y`：本次核身为 3DS 挑战
- `is3DS=N`：非 3DS 核身（密码 / 免密）
- 执行顺序：**协议查询与预路由在 `confirmPayInfo` 阶段完成**，**核身（is3DS）在后续 `verify` 阶段产生**——先协议与预路由，再核身。

## preferSign 来源与取值

满足任一来源即视为 `preferSign=Y`：

- **支付鉴权透传**：`authpay` 按商户组、产品码、支付场景、入口、版本号返回鉴权结果，携带 `preferSign` 字段（`Y` / `N` / `null`）。
- **全局配置（2023-8 新增）**：当 `alwaysPreferSign=true` 且卡为借记卡时，不关注鉴权结果，强制 `preferSign=Y`。
  - 老收银台：`cashdesk-api.yml → cashdesk.alwaysPreferSign`
  - 新收银台：`gp193_cashierii.yml → cashier.alwaysPreferSign`

取值含义：

| 值 | 含义 |
|---|---|
| `Y` | 优先签约 / 订阅 |
| `N` | 鉴权明确配置为不优先签约 |
| `Null` | 鉴权未命中 / 未配置，按不签约处理 |

## 交易类型判定

- `preferSign=Y` 且核身=3DS → **签约交易 → CKO102**；签约渠道不可用则降级 **CKO101 且不签约**。
- `preferSign=Y` 且核身=非 3DS 且用户已有签约协议 → **订阅（代扣）支付 → CKO111**，渠道侧传 `frictionless=Y`。
- `preferSign=N` 或 `Null` → 不签约、不走订阅渠道，按普通渠道处理。

## CKO 渠道角色

| 渠道 | 角色 | 核身要求 |
|---|---|---|
| CKO101 | 支付渠道 | 必须 3DS；无签约能力 |
| CKO102 | 签约渠道 | 必须 3DS；绑卡支付同时签约 |
| CKO111 | 协议 / 订阅 | 非 3DS（密码 / 免密）；要求卡上已有有效签约 |
| CKO121 | 绑卡渠道 | 必须 3DS；独立绑卡 + 签约，不参与支付路由 |

## router 渠道得分 + 扩展参数匹配

router 通过两层控制选定渠道：

1. **渠道得分**：签约渠道得分高于普通 3DS 渠道。
2. **扩展参数匹配**：按 `preferSign` 与 `is3DS` 过滤出签约 3DS 渠道或普通 3DS 渠道。

收银台传参与最终渠道：

| 收银台传参 | 签约渠道是否可用 | 最终渠道 |
|---|---|---|
| `preferSign=Y, is3ds=Y` | 可用 | 签约渠道 |
| `preferSign=Y, is3ds=Y` | 不可用 | 普通 3DS |
| `preferSign=N / Null, is3ds=Y` | 可用 | 普通 3DS |
| `preferSign=N / Null, is3ds=Y` | 不可用 | 普通 3DS |

## 签约支付流程

1. router 按规则过滤出签约 3DS 渠道或普通 3DS 渠道。
2. 渠道完成 3DS 交易；命中签约渠道时向收银台发绑卡消息（携带签约号、`signSource=CKO`）。
3. 收银台将签约信息存入 member（[[tbl_member_tr_bank_card_token]]，`signTransactionId` 加密为 `token`）。
4. CMF 向 payment 返回结果，完成交易。

## 代扣 / 订阅支付流程

1. 收银台查询渠道侧是否有可用的已签约渠道（router 过滤规则实现）。
2. 收银台传 `frictionless=Y && is3ds=N` 表示代扣支付。
3. 渠道通过 member 查询已签约协议号，发起支付并返回结果。

完整时序见 [[flow_cko_subscription_payment]]。

## 收银台传参链路（决策点）

- `confirmPayInfo`：
  - 鉴权区分 `card_pay`（已绑卡）/ `quick_pay`（新绑卡）；`paychannel=15` 本地卡 / AE，`30` 外卡。
  - 按 `preferSign` + 卡场景判断是否查卡签约数据（日志：**查询卡签约渠道**）——绑卡不查，已存卡查。
  - 按 `preferSign` + 用户协议结果判断是否预路由（日志：**订阅支付渠道预路由**）。
  - 按路由结果调风控支付事件传 `frictionless`（仅"支持订阅 + 已签约 + 签约渠道可用"时 `frictionless=Y`）。
- `verify`：
  - 按 `preferSign` + 核身给 CMF 传参（仅"支持订阅 + 已签约 + 签约渠道可用 + 核身非 3DS"时 `frictionless=Y`）。
  - 渠道返回 `signTransactionId`、`signSource`，前端据此认定签约渠道。
- 新收银台 verify 给 CMF 传 `CardTokenCreateRequest`：
  - 未签约且支持订阅 → `preferSign=Y`
  - 已签约且非 3DS → 传 `is3DS`，router 按参数过滤路由

## 路由结果速查矩阵

以"支付绑卡 / 已绑卡"场景为例：

| preferSign | 核身 | 签约状态 | 签约渠道可用 | 路由结果 |
|---|---|---|---|---|
| Y | 3DS | 新卡 / 未签 | 可用 | **CKO102 签约** |
| Y | 3DS | 新卡 / 未签 | 不可用 | CKO101 |
| Y | 密码 / 免密 | 未签约 | 可用 | 非 CKO102 |
| Y | 3DS | 已签约 | 可用 | CKO101（卡支付） |
| Y | 3DS | 已签约 | 不可用 | CKO102 重签 |
| Y | 密码 / 免密 | 已签约 | 可用 | **CKO111 订阅** |
| Y | 密码 / 免密 | 已签约 | 不可用 | 非 CKO111 |
| N / Null | 3DS | 任意 | 可用 | CKO101 |
| N / Null | 密
