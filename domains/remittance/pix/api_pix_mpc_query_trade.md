---
id: api_pix_mpc_query_trade
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
name: 查询MPC交易接口 (/pix/mpc/v1/query-trade)
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
支付成功后（收银台结果页跳转到 MPC 结果页时），由 wallet 调用，用于查询 MPC 交易信息以便在结果页展示。

## 路径/方法
- 路径：`/pix/mpc/v1/query-trade`
- 所属系统：pix
- 下游实现：`MpcFacade.parseCode`（pix-channel，dubbo facade）
- CGS API Doc：TODO

## 入参
原文未提供。

## 出参
原文未提供（仅说明返回交易信息用于结果页展示）。

## 错误码
原文未提供。

## 测试校验点
- 在 cashier 支付成功后调用，能正确返回交易信息以供 MPC 结果页展示。
- 调用链路：wallet → pix `/pix/mpc/v1/query-trade` → pix-channel `MpcFacade.parseCode` 实现。
