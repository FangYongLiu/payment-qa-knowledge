---
title: CKO渠道订阅支付业务总览
domain: channel-integration
kind: wiki_page
slug: cko-subscription-payment-overview
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:AQ/2228977707
tags: []
---

# CKO渠道订阅支付业务总览

本页介绍 CKO 渠道订阅支付的业务背景、核心概念与四个 CKO 子渠道（CKO101/102/111/121）的定位与适用范围。

## 业务背景

面向"支付鉴权配置支持订阅支付"的指定业务：当用户使用已签约的银行卡、原本走 moto 渠道完成支付时，可路由到 CKO 对应的签约渠道（如 CKO111）完成订阅 / 代扣支付。可理解为在原有支付能力上**新增了一个 moto（订阅）渠道**。

## 路由决策三要素

订阅支付的渠道路由由以下三要素共同决定：

> **preferSign 传参** + **用户是否已有签约协议** + **核身项（is3DS / 密码 / 免密）** ⟹ 决定路由渠道

其中 `is3DS=Y` 表示本次核身为 3DS，`is3DS=N` 表示非 3DS（如密码 / 免密）。

详细的路由判定规则与得分机制见 [[cko-subscription-routing-mechanism]]。

### preferSign 的来源（满足其一即 Y）

- **支付鉴权透传**：authpay 按商户组、产品码、支付场景、入口、版本号返回鉴权结果，携带 `preferSign` 字段（Y / N / null）。
- **全局配置（2023-8 新增）**：当 `alwaysPreferSign=true` 且卡为借记卡时，不关注鉴权结果，强制 `preferSign=Y`。配置位置：
  - 老收银台：`cashdesk-api.yml → cashdesk.alwaysPreferSign`
  - 新收银台：`gp193_cashierii.yml → cashier.alwaysPreferSign`

### preferSign 取值含义

| 取值 | 含义 |
|---|---|
| `Y` | 优先签约 / 订阅 |
| `N` | 支付鉴权明确配置为不优先签约 |
| `Null` | 支付鉴权未命中 / 未配置该字段，按不签约处理 |

### 交易类型判定

- `preferSign=Y` 且核身=3DS：**签约交易** → CKO102；签约渠道不可用则降级 CKO101 且不签约。
- `preferSign=Y` 且核身=非 3DS 且用户已有签约协议：**订阅（代扣）支付** → CKO111，渠道侧传 `frictionless=Y`。
- `preferSign=N` 或 `Null`：不签约、不走订阅渠道，按普通渠道处理。

### 执行顺序

协议查询与预路由在 `confirmPayInfo` 阶段完成，核身（is3DS）在其后的 `verify` 阶段产生——**先协议与预路由，再核身**。收银台交互细节见 [[cko-subscription-cashier-flow]]。

## CKO 渠道定义

| 渠道 | 角色 | 说明 / 核身要求 |
|---|---|---|
| **CKO101** | 支付渠道 | 不具备签约能力；核身必须为 3DS |
| **CKO102** | 签约渠道 | 边支付边签约；核身必须为 3DS |
| **CKO111** | 协议 / 订阅 | 非 3DS 核身（密码 / 免密）；要求该卡已有有效签约 |
| **CKO121** | 绑卡渠道 | 绑卡鉴权 + 签约；仅独立绑卡使用；核身必须为 3DS |

## 业务范围

### 绑卡方式

- **独立绑卡**（wallet → card）：固定 CKO121，不受配置影响。
- **支付绑卡**（收银台添加卡）：走 CKO101 / 102 / 111。

### 收银台

- **老收银台 cashdesk**：PayBy App。
- **新收银台 cashierii**：BotIM（含充值，已迁移至新收银台）。

### 特殊业务

付款码、代扣支付、authSign、facepay、国际汇款。

### 不支持

PayPage（含匿名支付）不支持订阅支付。

## 路由结果速查矩阵

以"支付绑卡 / 已绑卡"场景为例：

| preferSign | 核身 | 签约状态 | 签约渠道可用 | 路由结果 |
|---|---|---|---|---|
| Y | 3DS | 新卡 / 未签 | 可用 | CKO102 签约 |
| Y | 3DS | 新卡 / 未签 | 不可用 | CKO101 |
| Y | 密码 / 免密 | 未签约 | 可用 | 非 CKO102 |
| Y | 3DS | 已签约 | 可用 | CKO101（卡支付） |
| Y | 3DS | 已签约 | 不可用 | CKO102 重签 |
| Y | 密码 / 免密 | 已签约 | 可用 | **CKO111 订阅** |
| Y | 密码 / 免密 | 已签约 | 不可用 | 非 CKO111 |
| N / Null | 3DS | 任意 | 可用 | CKO101 |
| N / Null | 密码 | 已签约 | 可用 | 非 CKO111 |

> 关键规律：`preferSign=Y` 且 `is3DS=Y` 才触发签约；已签约卡走密码 / 免密命中 CKO111；`preferSign=N / Null` 一律不签约、不走订阅渠道。

## 相关链接

- 时序流程：[[flow_cko_subscription_payment]]
- 路由决策机制：[[cko-subscription-routing-mechanism]]
- 收银台交互流程：[[cko-subscription-cashier-flow]]
- 测试方法：[[cko-subscription-test-guide]]
- 测试卡用例：[[scn_cko_subscription_test_cards]]
- 关键数据表：[[tbl_member_tr_bank_card_token]]、[[tbl_member_tr_deduct_channel]]、[[tbl_deduct_t_deduct_protocol]]、[[tbl_protocol_t_contract_sign_info]]、[[tbl_cashdesk_t_filter_node]]
