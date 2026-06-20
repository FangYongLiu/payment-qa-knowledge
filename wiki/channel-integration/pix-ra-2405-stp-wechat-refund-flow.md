---
title: pix-RA-2405-STP-Wechat 退款时序流程
domain: channel-integration
kind: wiki_page
slug: pix-ra-2405-stp-wechat-refund-flow
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:0c609e41-a9fd-4515-bf2f-9c82c4cce6e7
tags: []
---

# pix-RA-2405-STP-Wechat 退款时序流程

本页描述外商通过 Tenpay 渠道发起退款时，由 pix 作为中心编排组件协调 tradeii 与 query 完成端到端退款处理的时序。

## 参与方

- **Foreign Merchant**：退款发起方（外商）
- **vendor(Tenpay)**：渠道侧供应商
- **pix**：中心编排组件（退款流程的 orchestrator）
- **tradeii**：实际退款处理服务
- **query**：退款账单通知接收方

## 时序步骤

请求链路（实线箭头表示请求调用）：

1. **1 apply refund**：Foreign Merchant → vendor(Tenpay)，外商向 Tenpay 申请退款
2. **1.1 refund**：vendor(Tenpay) → pix，Tenpay 将退款请求转发至 pix
3. **1.1.1 refund**：pix → tradeii，pix 将退款下发至 tradeii
4. **1.1.1.1 process refund**：tradeii 自调用，执行退款处理逻辑
5. **1.1.1.2**：tradeii → pix，返回处理结果（虚线响应）
6. **1.1.2 notify refund bill**：pix → query，通知 query 服务退款账单
7. **1.1.3**：pix → vendor(Tenpay)，返回响应（虚线响应）
8. **1.1.4**：vendor(Tenpay) → Foreign Merchant，最终响应回传至外商（虚线响应）

## 流程要点

- 调用方向：Merchant → Tenpay → pix → tradeii，逐层下发；响应沿原路径反向回传
- pix 在整个流程中作为中心编排者：既向 tradeii 分发实际退款处理，又向 query 异步通知退款账单
- 实线箭头代表请求调用，虚线箭头代表响应返回
- query 仅接收 `notify refund bill`，不参与请求链路上的同步响应
