---
id: api_pix_mpc_query_trade
object_type: API
domain: card
status: active
owner: unassigned
reviewer: unassigned
last_reviewed_at: '2026-06-20'
source_type: wiki
source_ref: confluence:PMDPayment/517832723
tags:
- PIX
- MPC
- query-trade
subdomain: pix
module: mpc
sensitivity: normal
name: MPC查询交易接口 (/pix/mpc/v1/query-trade)
aliases: []
related_services:
- svc_query
---

## 用途
在 MPC 扫码支付完成后（收银台支付成功，跳转到 MPC 结果页时），由钱包调用以查询交易信息，用于呈现交易结果。

## 路径/方法
- 路径：`/pix/mpc/v1/query-trade`
- 所属系统：pix
- 调用方：wallet
- 后端实现：`MpcFacade.parseCode`（pix-channel 实现 dubbo facade）

## 入参
原文未提供详细入参定义（CGS API Doc: TODO）。

## 出参
原文未提供详细出参定义（CGS API Doc: TODO）。返回内容用于支撑 MPC 结果页展示交易信息。

## 错误码
原文未列出。

## 测试校验点
- 在收银台支付成功后跳转到 MPC 结果页时调用，能够正确返回交易信息。
- 与 `/pix/mpc/v1/create-trade` 创建的交易对应，可查询到该交易状态与结果。
- pix-channel 侧 `MpcFacade.parseCode` dubbo facade 实现可被正确调用。
