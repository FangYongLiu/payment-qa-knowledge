---
title: CKO订阅支付收银台交互流程
domain: channel-integration
kind: wiki_page
slug: cko-subscription-cashier-flow
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:AQ/2228977707
tags: []
---

# CKO订阅支付收银台交互流程

本页梳理老收银台（PayBy App / cashdesk）与新收银台（BotIM / cashierii）在 `unityInitPayPage` → `confirmPayInfo` → `verify` 三阶段对 `preferSign`、`frictionless`、`is3DS` 的判定与传参逻辑。路由决策原理与渠道角色见 [[cko-subscription-routing-mechanism]]。

## 阶段顺序与核心字段

- 阶段顺序：协议查询与预路由在 `confirmPayInfo` 完成；核身（is3DS）在其后的 `verify` 阶段产生 —— 先协议与预路由，再核身。
- `preferSign` 取值：`Y` 优先签约 / 订阅；`N` 明确不签约；`Null` 未命中规则，按不签约处理。
- `preferSign` 来源（满足其一即 Y）：
  - 支付鉴权透传：authpay 按商户组、产品码、支付场景、入口、版本号返回，配置见 [[tbl_cashdesk_t_filter_node]]。
  - 全局配置（2023-8 新增）：`alwaysPreferSign=true` 且为借记卡时强制 `preferSign=Y`。
    - 老收银台：`cashdesk-api.yml → cashdesk.alwaysPreferSign`
    - 新收银台：`gp193_cashierii.yml → cashier.alwaysPreferSign`

## 老收银台流程（PayBy App / cashdesk）

### ① /cashdesk/unityInitPayPage

- 调用 authpay，返回命中的鉴权结果（含支持的支付方式与 `preferSign`：`Y / N / null`）。
- 鉴权结果缓存在 `paymentMethod`。
- 鉴权区分 `card_pay`（已绑卡） / `quick_pay`（新绑卡）。
- `paychannel=15` 本地卡 / AE，`paychannel=30` 外卡。

### ② /cashdesk/confirmPayInfo

- 全局配置兜底：`alwaysPreferSign=true` 且借记卡时，不看鉴权结果，默认 `preferSign=Y`。
- 按 `preferSign` + 卡场景判断是否查卡签约数据（日志关键字：**查询卡签约渠道**）：
  - 绑卡（新卡）不查；已存卡查。
  - 数据来源 [[tbl_member_tr_bank_card_token]]。
- 按 `preferSign` + 用户协议结果判断是否预路由（日志关键字：**订阅支付渠道预路由**）。
- 按预路由结果调风控支付事件并传 `frictionless`：
  - 仅当「支持订阅 + 已签约 + 签约渠道可用」时 `frictionless=Y`。

### ③ /cashdesk/verify

- 按 `preferSign` + 核身结果给 CMF 传参：
  - 仅当「支持订阅 + 已签约 + 签约渠道可用 + 核身非 3DS」时 `frictionless=Y`。
- 渠道侧返回 `signTransactionId`、`signSource`，前端据此认定签约渠道。

## 新收银台流程（cashierii / BotIM）

含充值业务（已迁移至新收银台）。

- 查询卡信息，结合鉴权结果判断命中规则；按规则 `preferSign` 决定是否查用户签约协议（日志：**查询卡签约渠道**）。
- 按协议结果判断是否调预路由（日志：**订阅支付渠道预路由**）。
- GRC 支付事件 `frictionless=null / Y`。
- GRC 按规则返回是否 3DS；后续渠道按 `is3DS` 路由。
- `verify` 阶段按「用户是否签约 + 风控审核结果」给 CMF 传 `CardTokenCreateRequest`：
  - 未签约且支持订阅 → `preferSign=Y`。
  - 已签约且非 3DS → 传 `is3DS`，由 router 按参数过滤路由。

## 三参数组合与路由结果

收银台传参直接决定 router 的渠道过滤；完整时序见 [[flow_cko_subscription_payment]]。

| preferSign | is3DS | frictionless | 含义 | 典型路由 |
|---|---|---|---|---|
| Y | Y | — | 新卡签约 | CKO102（不可用降级 CKO101） |
| Y | N | Y | 已签约卡订阅 / 代扣 | CKO111 |
| N / Null | Y | — | 普通 3DS 支付 | CKO101 |
| N / Null | N | — | 不签约、不订阅 | 普通渠道 |

完整矩阵（覆盖签约渠道可用 / 不可用、已签 / 未签等场景）参见 [[cko-subscription-payment-overview]] 与 [[cko-subscription-routing-mechanism]]。

## 签约支付的回写动作

`verify` 命中签约渠道后，CMF / 渠道向收银台发送绑卡消息（携带签约号、`signSource=CKO`），收银台将签约信息存入 member 库的 [[tbl_member_tr_bank_card_token]]（`signTransactionId` 加密为 `token`），作为后续判断「卡是否已签约」的依据。

## 调试关键日志与字段

- **查询卡签约渠道**：判定是否依据已存卡查询签约数据。
- **订阅支付渠道预路由**：判定是否进行订阅渠道预路由。
- 各接口入参 `preferSign` / `frictionless` / `is3DS`。
- CMF 返回 `signTransactionId` / `signSource`。

测试方法、测试卡号与核身规则配置见 [[cko-subscription-test-guide]]，用例样例见 [[scn_cko_subscription_test_cards]]。

## 不支持范围

- PayPage（含匿名支付）不支持订阅支付：在 `unityInitPayPage` 阶段不进入上述 preferSign / 预路由分支。
