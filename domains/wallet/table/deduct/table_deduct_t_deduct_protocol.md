---
id: tbl_deduct_t_deduct_protocol
object_type: Table
domain: wallet
status: active
owner: unassigned
reviewer: unassigned
last_reviewed_at: '2026-06-19'
source_type: wiki
source_ref: confluence:AQ/2228977707
tags:
- deduct
- protocol
- subscription
- autodebit
subdomain: deduct
module: null
sensitivity: normal
name: 代扣协议表 t_deduct_protocol
aliases:
- t_deduct_protocol
related_services:
- svc_protocol
---

## 用途
代扣协议表，库为 deduct。在 `paySceneCode=PAYANDSIGN`（支付并签代扣）场景成功后落库，用于持久化代扣协议数据；其 `deduct_protocol_no` 可作为后续 `paySceneCode=AUTODEBIT`（代扣）交易的 `authProtocolNo` 入参，发起免交互的代扣支付。

## 关键列
- `deduct_protocol_no`：代扣协议号。PAYANDSIGN 成功后写入，可用于 AUTODEBIT 代扣发起。

## 主键/索引
原文未提供。

## 校验点(QA 关注)
- PAYANDSIGN 收单（`protocolSceneCode=111`）成功后，校验 `t_deduct_protocol` 是否新增记录、`deduct_protocol_no` 是否生成。
- 取该 `deduct_protocol_no` 作为 AUTODEBIT 的 `authProtocolNo`，应能直接完成代扣（无用户交互）。
- 协议号来源对比：`t_deduct_protocol.deduct_protocol_no`（代扣场景）与 `t_contract_sign_info.sign_contract_no`（签约协议号）属不同来源，不要混用。
- 仅 PAYANDSIGN 场景才落 `t_deduct_protocol`；普通收单 DYNQR、匿名 PAYPAGE 不应产生该表记录。
