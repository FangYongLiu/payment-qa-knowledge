---
title: CKO支付渠道定义(101/102/111/121)
domain: channel-integration
kind: wiki_page
slug: cko-channel-definitions
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki
source_ref: wiki:5b35d40b-b532-44de-b69e-abffc289be85
tags: []
---

# CKO支付渠道定义(101/102/111/121)

本页定义 CKO 在订阅支付能力下的四个渠道角色、核身要求与适用场景，作为路由决策的基础。整体业务背景见 [[cko-subscription-payment-overview]]，路由参数与流转见 [[cko-subscription-system-flow]]。

## 渠道一览

| 渠道 | 角色 | 核身要求 | 说明 |
|---|---|---|---|
| CKO101 | 支付渠道 Payment | 必须 3DS | 不具备签约能力，仅完成支付 |
| CKO102 | 签约渠道 Signing | 必须 3DS | 绑卡并同时签约（bind-and-pay while signing） |
| CKO111 | 协议 / 订阅渠道 Subscription | 非 3DS（密码 / 免密） | 要求卡上已存在有效签约协议 |
| CKO121 | 绑卡渠道 Card-binding | 必须 3DS | 独立绑卡 + 签约，仅用于独立绑卡场景 |

## 各渠道适用场景

### CKO101（支付）
- 不签约、不走订阅渠道时的普通 3DS 支付。
- 当 `preferSign=Y` 但签约渠道不可用时，降级到 CKO101，且不签约。
- `preferSign=N / Null` 且 `is3DS=Y` 时一律走 CKO101。
- 已签约卡若以 3DS 方式支付，也走 CKO101（按卡支付处理，不复签）。

### CKO102（签约）
- 触发条件：`preferSign=Y` 且核身=3DS 且卡未签约。
- 渠道完成 3DS 交易后，向收银台发绑卡消息（带签约号、`signSource=CKO`）。
- 收银台据此将签约信息写入 `tr_bank_card_token`（`signTransactionId` 加密为 `token`）。
- 若已签约卡场景下签约渠道不可用，可走 CKO102 重签。

### CKO111（订阅 / 代扣）
- 触发条件：`preferSign=Y` 且核身=非 3DS（密码 / 免密）且用户已有签约协议且签约渠道可用。
- 渠道侧关键参数：`frictionless=Y`、`is3ds=N`。
- 渠道通过 member 查询已签约协议号后发起支付。
- 不支持场景：PayPage（含匿名支付）不支持订阅支付，因此不会路由到 CKO111。

### CKO121（独立绑卡）
- 仅用于独立绑卡入口（wallet→card），固定走 CKO121，不受支付鉴权 `preferSign` 配置影响。
- 完成绑卡认证 + 签约，签约成功后写入 `tr_deduct_channel`。
- 必须 3DS 核身。

## 与路由决策的关系

四个渠道由 router 通过「渠道得分 + 扩展参数匹配」筛选：签约渠道得分高于普通 3DS 渠道，再以 `preferSign` 与 `is3DS` 过滤出最终渠道。详见 [[cko-subscription-system-flow]]。

路由结果速查（支付绑卡 / 已绑卡场景）：

| preferSign | 核身 | 签约状态 | 签约渠道 | 路由结果 |
|---|---|---|---|---|
| Y | 3DS | 未签 | 可用 | CKO102 签约 |
| Y | 3DS | 未签 | 不可用 | CKO101 |
| Y | 密码 / 免密 | 未签约 | 可用 | 非 CKO102 |
| Y | 3DS | 已签约 | 可用 | CKO101（卡支付） |
| Y | 3DS | 已签约 | 不可用 | CKO102 重签 |
| Y | 密码 / 免密 | 已签约 | 可用 | CKO111 订阅 |
| Y | 密码 / 免密 | 已签约 | 不可用 | 非 CKO111 |
| N / Null | 3DS | 任意 | 可用 | CKO101 |
| N / Null | 密码 | 已签约 | 可用 | 非 CKO111 |

要点：
- 仅当 `preferSign=Y` 且 `is3DS=Y` 时才触发签约（CKO102）。
- 已签约卡走密码 / 免密时命中 CKO111。
- `preferSign=N / Null` 一律不签约、不走订阅渠道。

## 业务范围与限制

- **绑卡方式**：独立绑卡固定 CKO121；支付绑卡走 CKO101 / 102 / 111。
- **收银台**：老收银台 cashdesk（PayBy App）、新收银台 cashierii（BotIM，含充值，已迁移）。
- **特殊业务**：付款码、代扣支付、authSign、facepay、国际汇款。
- **不支持**：PayPage（含匿名支付）不支持订阅支付，因此不路由 CKO111。

## 测试与验证

- 渠道路由结果是订单维度的核心校验项，需结合 `tr_bank_account`、`tr_bank_card_token`、`tr_deduct_channel` 等表确认渠道与协议号写入。
- 用例与数据校验方法见 [[cko-subscription-test-guide]] 与 [[scn_cko_subscription_payment_cases]]；端到端流程见 [[flow_cko_subscription_payment]]。
