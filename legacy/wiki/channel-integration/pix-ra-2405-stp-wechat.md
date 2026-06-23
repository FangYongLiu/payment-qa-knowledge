---
title: pix-RA-2405-STP-Wechat Wechat STP关闭支付流程
domain: channel-integration
kind: wiki_page
slug: pix-ra-2405-stp-wechat
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:3d1841f6-1d45-4dc2-bad7-f9ba31b236b0
tags: []
---

# pix-RA-2405-STP-Wechat Wechat STP关闭支付流程

本页描述 Wechat STP 场景下，Tenpay 发起 close payment 时 pix 与 tradeii 的交互时序。

## 参与方

- **vendor(Tenpay)**：发起关闭支付请求的渠道方。
- **pix**：接收并编排关闭支付流程的服务。
- **tradeii**：负责交易过期处理的下游服务。

## 时序流程

1. **close payment**：vendor(Tenpay) → pix，发起关闭支付请求。
2. **1.1 TradeOptionalFacade#expireTrade**：pix → tradeii，调用过期交易接口。
3. **1.2**：tradeii → pix，返回处理结果。
4. **1.3**：pix → vendor(Tenpay)，将结果回传给渠道方。

## 关键点

- pix 在收到 close payment 后，将交易过期处理委托给 tradeii，通过 `TradeOptionalFacade#expireTrade` 完成。
- 调用结果按调用链原路返回至 vendor(Tenpay)。
