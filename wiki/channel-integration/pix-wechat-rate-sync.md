---
title: PIX微信渠道汇率同步与计算规则
domain: channel-integration
kind: wiki_page
slug: pix-wechat-rate-sync
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki
source_ref: wiki:a68e3cf4-694f-4d32-9a67-4b4aaeee8675
tags: []
---

# PIX微信渠道汇率同步与计算规则

本页说明 PIX 微信 MPC 渠道中，AED 到本地币种（CNY）的基础汇率如何从 remittance 同步、margin 如何配置，以及客户实付金额（Pay Amount）的计算规则。

## 汇率同步机制

- 通过 dubbo api 周期性从 remittance 服务同步汇率配置。
- 仅当查询到的汇率与当前不同才更新。
- 系统设计参考：`pix-SD-FX Rate`。
- 渠道接入与系统流程参见 [[pix-wechat-mpc-overview]] 与 [[pix-wechat-system-flow]]。

## 关键概念

- **Exchange Rate**：AED 到本地币种的基础汇率，来源于 remittance。
- **Rate Margin Percent**：在基础汇率上叠加的利润 margin，按渠道配置。
- **Customer Rate**：对客实际换算汇率，由基础汇率与 margin 计算得出。

## Margin 配置职责分工

| 模块 | 职责 |
|---|---|
| pix | 周期性从 remittance 查询汇率并更新；提供 margin 配置 dubbo API |
| remittance | 提供基础汇率查询 |
| basis-customer | 提供查询汇率的 UI；提供查询与配置 margin 的 UI |

## 计算规则

以 WECHAT 渠道为例：

- Exchange Rate = `1.96688000`
- Margin Percent = `0.01`
- Transaction Amount = `200 CNY`

计算步骤：

1. **Customer Rate** = `Exchange Rate × (1 - Margin Percent)`
   - = `1.96688000 × (1 - 0.01)` = `1.9472112`
2. **Pay Amount** = `Transaction Amount / Customer Rate`
   - = `200 / 1.9472112` = `102.7109950887711` ≈ `102.72`

> 取整规则（Round up / Ceiling）待确认（TODO）。
> Profit 计算方式待确认（TODO）。

## 视图区分

- **Customer View**：展示给用户的汇率为 Customer Rate（已扣除 margin）。
- **Inner View**：内部留存基础 Exchange Rate 与 Margin Percent，用于核算与利润统计。

## 退款金额换算

退款时不再重新换汇，按原单等比折算：

- `Refund Pay Amount = Refund Transaction Amount / Original Transaction Amount × Original Pay Amount`

详见 [[flow_pix_wechat_refund]]。

## 关联

- 钱包侧根据该汇率规则计算待支付的 AED 金额，再进入下单流程，详见 [[flow_pix_wechat_mpc_payment]]。
- 字段与 API 细节参见 [[pix-wechat-vendor-api-catalog]] 与 [[pix-wechat-qa-notes]]。
