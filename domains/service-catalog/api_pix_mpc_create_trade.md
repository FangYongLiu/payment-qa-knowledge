---
id: api_pix_mpc_create_trade
object_type: API
domain: service-catalog
status: active
owner: unassigned
reviewer: unassigned
last_reviewed_at: '2026-06-20'
source_type: wiki
source_ref: confluence:PMDPayment/517832723
tags:
- PIX
- MPC
- create-trade
subdomain: pix
module: mpc
sensitivity: normal
name: MPC创建交易接口 (/pix/mpc/v1/create-trade)
aliases: []
related_services:
- svc_pix
---

## 用途
在 MPC 商户呈现码支付流程中，由 wallet 在用户确认交易信息（可选输入金额、按汇率计算本地金额）后调用，用于（可选地）创建交易并返回 cashierToken，同时基于费率配置（rate config）对金额进行校验。

## 路径/方法
- 路径：/pix/mpc/v1/create-trade
- 系统：pix
- 调用方：wallet
- 下游 dubbo facade：MpcFacade.parseCode（由 pix-channel 实现）

## 入参
原文未提供具体入参字段。可推断的上下文输入：
- 来自 /pix/mpc/v1/parse 返回的 code id
- （可选）用户输入的支付金额

## 出参
- cashierToken：用于后续进入 cashier 支付流程

## 错误码
原文未提供。

## 测试校验点
- 创建交易后必须返回 cashierToken，供后续 cashier 支付流程使用
- 金额需结合 rate config 进行校验（Check amount with rate config）
- 创建交易步骤为可选（Optional）：在需要用户输入金额或基于汇率换算本地金额的场景下触发
- 后续支付完成后通过 /pix/mpc/v1/query-trade 可查询到该交易信息
- pix 侧通过 MpcFacade（dubbo facade）调用 pix-channel 的实现
