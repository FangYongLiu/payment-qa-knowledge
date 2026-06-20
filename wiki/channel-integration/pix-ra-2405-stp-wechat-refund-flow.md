---
title: PIX RA-2405 STP微信渠道退款流程
domain: channel-integration
kind: wiki_page
slug: pix-ra-2405-stp-wechat-refund-flow
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:ef74365a-3441-4700-9b08-5ea12526da65
tags: []
---

# PIX RA-2405 STP微信渠道退款流程

本页描述外部商户（Foreign Merchant）通过 vendor(Tenpay) 发起退款，经 pix 路由分发至 tradeii 实际处理、并通知 bill 的端到端调用时序。pix 作为本流程的核心路由系统。

## 参与方

- **Foreign Merchant**：发起退款的外部商户
- **vendor(Tenpay)**：微信渠道供应商
- **pix**：路由与编排系统（本流程焦点）
- **tradeii**：退款处理系统
- **bill**：账单/账务通知系统

## 时序步骤

按 UML 顺序图编号自上而下：

1. `1: apply refund` — Foreign Merchant → vendor(Tenpay)：商户向微信渠道申请退款（同步）
2. `1.1: refund` — vendor(Tenpay) → pix：Tenpay 将退款请求转发至 pix（同步）
3. `1.1.1: refund` — pix → tradeii：pix 将退款下发到 tradeii（同步）
4. `1.1.1.1: process refund` — tradeii → tradeii：tradeii 内部自处理退款（自循环）
5. `1.1.1.2:` — tradeii ⇠ pix：tradeii 向 pix 返回处理结果（异步/返回）
6. `1.1.2: notify refund bill` — pix → bill：pix 通知 bill 系统记账（同步）
7. `1.1.3:` — pix ⇠ vendor(Tenpay)：pix 向 Tenpay 返回结果（返回）
8. `1.1.4:` — vendor(Tenpay) ⇠ Foreign Merchant：Tenpay 向商户回执结果（返回）

## 调用语义

- **实线箭头**：同步调用（步骤 1、1.1、1.1.1、1.1.1.1、1.1.2）
- **虚线箭头**：返回响应（步骤 1.1.1.2、1.1.3、1.1.4）
- **退款处理路径**：Foreign Merchant → vendor(Tenpay) → pix → tradeii
- **账务通知路径**：pix → bill（与返回链并行/串行触发）
- **结果回传链路**：tradeii → pix → vendor(Tenpay) → Foreign Merchant

## 关键要点

- pix 在流程中承担**路由 + 通知编排**双重职责：既将退款下发 tradeii，也负责向 bill 发起 `notify refund bill`
- tradeii 是退款的**实际处理方**，处理动作在其内部完成（`process refund` 自循环）
- bill 通知发生在 pix 收到 tradeii 返回之后、回执 vendor(Tenpay) 之前/同链路中（编号 1.1.2 位于 1.1.3 之前）
