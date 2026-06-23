---
title: 微信渠道汇率同步与计费规则
domain: channel-integration
kind: wiki_page
slug: pix-wechat-rate-sync
status: archived
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:PMDPayment/433881954
tags: []
---

# 微信渠道汇率同步与计费规则

本页说明微信MPC渠道在 pix 侧的汇率同步机制、margin 配置方式，以及客户汇率与支付金额的计算规则。相关接入背景见 [[pix-wechat-mpc-integration-overview]]，配置项见 [[pix-wechat-configuration]]。

## 汇率来源与同步机制

- 基础汇率来源：remittance 服务，按 AED → 当地币种维护。
- 同步方式：pix 通过 dubbo api 周期性向 remittance 查询基础汇率，发现与当前不一致时更新。
- 设计参考：pix-SD-FX Rate。

## 关键概念

- **Exchange Rate**：从 AED 到当地币种的基础汇率，由 remittance 同步。
- **Rate Margin Percent**：在基础汇率上叠加的利润 margin，按渠道单独配置。
- **Customer Rate**：对客户展示并用于计费的实际汇率，由基础汇率和 margin 计算得出。

## 配置职责分工

| 项目 | 系统 | 功能 |
| --- | --- | --- |
| 查询基础汇率 | remittance | 提供基础汇率查询能力 |
| 同步基础汇率 | pix | 周期性查询并更新 |
| 配置 margin | pix | 提供 dubbo api 用于查询与配置 margin |
| 汇率/margin UI | basis-customer | UI 查询基础汇率；UI 查询与配置 margin |

## 客户汇率与支付金额计算

以微信渠道为例，配置：

- Exchange Rate：`1.96688000`
- Margin Percent：`0.01`

计算规则：

- Customer Rate = Exchange Rate × (1 − Margin Percent)
  - 例：`1.96688000 × (1 − 0.01) = 1.9472112`
- Pay Amount = Transaction Amount / Customer Rate
  - 例：`200 / 1.9472112 = 102.7109950887711 ≈ 102.72`

> 进位规则（Round up 或 Ceiling）以及利润口径仍为 TODO。

## 退款金额换算

- Refund Pay Amount = Refund Transaction Amount / Original Transaction Amount × Original Pay Amount
- 即按原单的成交比例折算应退的 Pay Amount，避免重新走汇率。
- 退款流程详见 [[flow_pix_wechat_refund]]。

## 与其他流程的衔接

- 在 `MpcFacade.parseCode` 解析商户码时，会一并保存包括汇率信息在内的商户码信息至 ES；下单环节 `MpcFacade.creatTrade` 会基于该汇率配置进行金额校验。完整链路见 [[flow_pix_wechat_mpc_payment]]。
- 钱包侧在确认交易信息时，依据该汇率计算需支付的 AED 金额。
