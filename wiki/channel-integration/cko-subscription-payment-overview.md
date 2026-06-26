---
title: CKO渠道订阅支付业务总览
domain: channel-integration
kind: wiki_page
slug: cko-subscription-payment-overview
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki
source_ref: wiki:5b35d40b-b532-44de-b69e-abffc289be85
tags: []
related_services:
  - svc_3ds2
  - svc_authpay
  - svc_cashdesk_api
  - svc_cashierii
  - svc_qpay_cko
related_tables:
  - tbl_cashdesk_t_filter_node
---

# CKO渠道订阅支付业务总览

本页介绍 CKO 渠道订阅支付项目的业务背景、`preferSign` 字段来源与含义、路由三要素决策矩阵，以及业务支持范围与限制。

## 业务背景

面向「支付鉴权配置支持订阅支付」的指定业务：当用户使用已签约银行卡、原本走 moto 渠道完成支付时，可路由到 CKO 对应的签约渠道（如 CKO111）完成订阅 / 代扣支付。可理解为在原有支付能力上**新增了一个 moto（订阅）渠道**。

CKO 渠道角色划分参见 [[cko-channel-definitions]]。

## 路由决策三要素

最终路由由以下三项共同决定：

- **preferSign 传参**（Y / N / Null）
- **用户是否已有签约协议**
- **核身项**（is3DS=Y 表示 3DS；is3DS=N 表示密码 / 免密等非 3DS）

> 执行顺序：协议查询与预路由在 `confirmPayInfo` 阶段完成；核身（is3DS）在其后的 `verify` 阶段产生——**先协议与预路由，再核身**。

完整端到端流程见 [[flow_cko_subscription_payment]] 与 [[cko-subscription-system-flow]]。

## preferSign 来源

满足以下任一条件即视为 `preferSign=Y`：

- **支付鉴权透传**：`authpay` 按商户组、产品码、支付场景、入口、版本号返回鉴权结果，携带 `preferSign` 字段（Y / N / null）。
- **全局配置**（2023-8 新增）：当 `alwaysPreferSign=true` 且卡为借记卡时，不关注鉴权结果，强制 `preferSign=Y`。
  - 老收银台：`cashdesk-api.yml` → `cashdesk.alwaysPreferSign`
  - 新收银台：`gp193_cashierii.yml` → `cashier.alwaysPreferSign`

## preferSign 取值含义

| 取值 | 含义 |
|---|---|
| `Y` | 优先签约 / 订阅 |
| `N` | 支付鉴权明确配置为不优先签约 |
| `Null` | 支付鉴权未命中或未配置该字段，按不签约处理 |

## 交易类型判定

- `preferSign=Y` 且核身=3DS：**签约交易** → CKO102；签约渠道不可用则降级 CKO101 且不签约。
- `preferSign=Y` 且核身=非 3DS 且用户已有签约协议：**订阅（代扣）支付** → CKO111，渠道侧传 `frictionless=Y`。
- `preferSign=N` 或 `Null`：不签约、不走订阅渠道，按普通渠道处理。

## 路由结果速查矩阵

以「支付绑卡 / 已绑卡」场景为例：

| preferSign | 核身 | 签约状态 | 签约渠道可用 | 路由结果 |
|---|---|---|---|---|
| Y | 3DS | 新卡 / 未签 | 可用 | CKO102 签约 |
| Y | 3DS | 新卡 / 未签 | 不可用 | CKO101 |
| Y | 密码 / 免密 | 未签约 | 可用 | 非 CKO102 |
| Y | 3DS | 已签约 | 可用 | CKO101（卡支付） |
| Y | 3DS | 已签约 | 不可用 | CKO102 重签 |
| Y | 密码 / 免密 | 已签约 | 可用 | CKO111 订阅 |
| Y | 密码 / 免密 | 已签约 | 不可用 | 非 CKO111 |
| N / Null | 3DS | 任意 | 可用 | CKO101 |
| N / Null | 密码 | 已签约 | 可用 | 非 CKO111 |

**核心规则**：

- `preferSign=Y` 且 `is3DS=Y` 才触发签约；
- 已签约卡走密码 / 免密命中 CKO111；
- `preferSign=N / Null` 一律不签约、不走订阅渠道。

## 业务范围

### 绑卡方式

- **独立绑卡**（wallet→card）：固定走 CKO121，**不受配置影响**
- **支付绑卡**（收银台添加卡）：走 CKO101 / 102 / 111

### 收银台

- **老收银台 cashdesk**：PayBy App
- **新收银台 cashierii**：BotIM（含充值，已迁移至新收银台）

### 特殊业务

付款码、代扣支付、authSign、facepay、国际汇款。

### 不支持

**PayPage（含匿名支付）不支持订阅支付。**

## 相关页面

- [[cko-channel-definitions]]：CKO101 / 102 / 111 / 121 渠道定义与核身要求
- [[cko-subscription-system-flow]]：路由决策机制、签约 / 代扣系统流程与关键数据表
- [[cko-subscription-test-guide]]：测试卡号、收单测试、鉴权与核身配置
- [[scn_cko_subscription_payment_cases]]：覆盖五大模块的测试场景集
