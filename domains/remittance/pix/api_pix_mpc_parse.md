---
id: api_pix_mpc_parse
object_type: API
domain: remittance
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-20'
source_type: wiki
source_ref: wiki:f244c1d0-438b-46a8-be70-acdc8cfa85b4
tags:
- pix
- mpc
subdomain: pix
module: mpc
sensitivity: normal
name: 解析MPC二维码接口 (/pix/mpc/v1/parse)
aliases: []
related_services: []
related_tables: []
related_scenarios:
- flow_pix_mpc_payment
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
- 在 wallet 完成本地规则匹配后调用，由 pix 系统将 QrCode 匹配到对应的 vendor code。
- 调用 channel 实现获取商户与交易信息（包含 rate information 费率信息）。
- 向 wallet 返回 code id，供后续创建交易等流程使用。

## 路径/方法
- 路径：`/pix/mpc/v1/parse`
- 所属系统：pix
- 下游实现：`MpcFacade.parseCode`（pix-channel，dubbo facade）
- CGS API Doc：TODO

## 入参
- 原文未提供具体字段，CGS API Doc：TODO。

## 出参
- code id（返回给 wallet）
- 商户信息（merchant information）
- 交易信息（trade information），包含 rate information
- 其余字段：原文未提供，CGS API Doc：TODO。

## 错误码
- 原文未提供。

## 测试校验点
- QrCode 能否正确匹配到 vendor code。
- channel 实现 `MpcFacade.parseCode` 是否被正确调用并返回商户/交易信息。
- 返回结果中是否包含 rate information（费率信息）。
- 是否返回 code id 给 wallet，用于后续 `/pix/mpc/v1/create-trade` 等接口。
