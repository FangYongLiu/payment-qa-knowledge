---
id: api_pix_mpc_parse
object_type: API
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-20'
source_type: wiki
source_ref: confluence:PMDPayment/517832723
tags:
- pix
- mpc
- parse
subdomain: pix
module: mpc
sensitivity: normal
name: MPC解析接口 (/pix/mpc/v1/parse)
aliases:
- /pix/mpc/v1/parse
related_services:
- svc_pix
---

## 用途
- 匹配 QrCode 获取 vendor code
- 调用 channel 实现以获取商户与交易信息（包含 rate 费率信息）
- 向 wallet 返回 code id

## 路径/方法
- 路径：`/pix/mpc/v1/parse`
- 所属系统：pix
- 上游调用方：wallet
- 下游 dubbo facade 实现：`MpcFacade.parseCode`（pix-channel）
- CGS API Doc：TODO

## 入参
原文未提供，TODO（参见 CGS API Doc）。

## 出参
- code id（返回给 wallet）
- 商户信息（merchant information）
- 交易信息（trade information），含 rate 费率信息

## 错误码
原文未提供。

## 测试校验点
- 调用前置条件：wallet 已通过 `/pix/mpc/v1/get-rules` 获取并使用规则匹配 QrCode 成功
- 校验 QrCode 能否匹配并解析出 vendor code
- 校验返回结果包含 merchant、trade 与 rate 信息
- 校验返回 code id 给 wallet，可供后续 `/pix/mpc/v1/create-trade` 使用
- 校验 dubbo facade `MpcFacade.parseCode` 被正确调用
