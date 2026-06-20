---
title: CKO订阅支付系统流程
domain: channel-integration
kind: wiki_page
slug: cko-subscription-system-flow
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki
source_ref: wiki:5b35d40b-b532-44de-b69e-abffc289be85
tags: []
---

# CKO订阅支付系统流程

本页聚焦 CKO 订阅支付的系统侧路由实现：router 渠道得分与扩展参数过滤、签约支付与代扣支付的处理时序，以及新老收银台在 `confirmPayInfo` / `verify` 阶段的差异。业务背景与渠道定义见 [[cko-subscription-payment-overview]] 与 [[cko-channel-definitions]]。

## 路由决策机制（router）

渠道路由由 router 通过「**渠道得分 + 扩展参数匹配**」共同控制：

- 签约渠道（CKO102）的得分高于普通 3DS 渠道（CKO101）。
- 通过 `preferSign` 与 `is3DS` 的组合，过滤出"签约 3DS 渠道"或"普通 3DS 渠道"。

### 路由结果（is3ds=Y 场景）

| 收银台传参 | 签约渠道可用 | 最终渠道 |
| --- | --- | --- |
| preferSign=Y, is3ds=Y | 可用 | 签约渠道 |
| preferSign=Y, is3ds=Y | 不可用 | 普通 3DS |
| preferSign=N / Null, is3ds=Y | 可用 | 普通 3DS |
| preferSign=N / Null, is3ds=Y | 不可用 | 普通 3DS |

完整路由矩阵（含密码 / 免密、已签约/未签约组合）见 [[cko-subscription-payment-overview]]。

## 签约支付时序

1. router 按规则过滤出签约 3DS 渠道或普通 3DS 渠道。
2. 渠道完成 3DS 交易；若命中签约渠道（CKO102），向收银台发**绑卡消息**，携带 `签约号` 与 `signSource=CKO`。
3. 收银台将签约信息写入 `member.tr_bank_card_token`，其中 `signTransactionId` 加密为 `token`。
4. CMF 将结果返回 payment，交易完成。

## 代扣 / 订阅支付时序

1. 收银台查询渠道侧是否存在可用的已签约渠道（由 router 过滤规则实现）。
2. 收银台传 `frictionless=Y && is3ds=N`，标识本次为代扣支付。
3. 渠道通过 `member` 查询已签约的协议号，发起支付并返回结果，命中 CKO111。

## 老收银台流程（cashdesk / PayBy App）

执行顺序：**协议查询与预路由在 `confirmPayInfo` 完成；核身（is3DS）在其后的 `verify` 产生**——先协议预路由，再核身。

### ① `/cashdesk/unityInitPayPage`
- 调用 authpay，返回命中的鉴权结果（含支持的支付方式与 `preferSign`：Y / N / null），缓存在 `paymentMethod`。

### ② `/cashdesk/confirmPayInfo`
- 全局配置（2023-8）：`alwaysPreferSign=true` 且为借记卡时，不看鉴权结果，强制 `preferSign=Y`。
- 鉴权区分 `card_pay`（已绑卡）/ `quick_pay`（新绑卡）；`paychannel=15` 本地卡 / AE，`30` 外卡。
- 按 `preferSign` + 卡场景判断是否查卡签约数据（日志：**查询卡签约渠道**）——绑卡不查，已存卡查。
- 按 `preferSign` + 用户协议结果判断是否预路由（日志：**订阅支付渠道预路由**）。
- 按路由结果调风控支付事件传 `frictionless`：仅"支持订阅 + 已签约 + 签约渠道可用"时 `frictionless=Y`。

### ③ `/cashdesk/verify`
- 按 `preferSign` + 核身向 CMF 传参；仅"支持订阅 + 已签约 + 签约渠道可用 + 核身非 3DS"时 `frictionless=Y`。
- 渠道返回 `signTransactionId`、`signSource`，前端据此认定为签约渠道。

## 新收银台流程（cashierii / BotIM）

1. 查询卡信息，结合鉴权结果判断命中规则；按规则 `preferSign` 决定是否查询用户签约协议（日志：**查询卡签约渠道**）。
2. 按协议结果判断是否调用预路由（日志：**订阅支付渠道预路由**）。
3. GRC 支付事件 `frictionless = null / Y`。
4. GRC 按规则返回是否 3DS；后续渠道按 `is3DS` 路由。
5. `verify` 阶段按"用户是否签约 + 风控审核结果"向 CMF 传 `CardTokenCreateRequest`：
   - 未签约且支持订阅 → `preferSign=Y`；
   - 已签约且非 3DS → 传 `is3DS`，由 router 按参数过滤路由。

## 新老收银台差异要点

| 维度 | 老收银台 cashdesk | 新收银台 cashierii |
| --- | --- | --- |
| 鉴权入口 | `unityInitPayPage` 调 authpay 缓存 `paymentMethod` | 查卡 + 鉴权结果联合命中规则 |
| `confirmPayInfo` | 卡签约查询 + 预路由 + 风控事件传 `frictionless` | 协议查询 + 预路由 + GRC 事件传 `frictionless` |
| 是否 3DS 决策 | 风控审核返回 | GRC 按规则返回 |
| `verify` 传参 | 按 `preferSign + 核身` 决定 `frictionless` | 通过 `CardTokenCreateRequest` 传 `preferSign` / `is3DS` |
| 签约判定依据 | 渠道返回 `signTransactionId`、`signSource` | 同上 |

## 关联

- 渠道角色与核身要求：[[cko-channel-definitions]]
- 端到端流程图：[[flow_cko_subscription_payment]]
- 测试操作与数据校验：[[cko-subscription-test-guide]]
- 用例集合：[[scn_cko_subscription_payment_cases]]
