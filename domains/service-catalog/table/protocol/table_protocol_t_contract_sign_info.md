---
id: tbl_protocol_t_contract_sign_info
object_type: Table
domain: service-catalog
status: active
owner: unassigned
reviewer: unassigned
last_reviewed_at: '2026-06-19'
source_type: wiki
source_ref: confluence:AQ/2228977707
tags:
- protocol
- contract
- sign
subdomain: protocol
module: null
sensitivity: normal
name: 签约协议信息表 t_contract_sign_info
aliases: []
related_services:
- svc_protocol
---

## 用途
位于 `protocol` 库，用于记录签约协议信息。在 CKO 订阅支付场景下，作为协议号(sign_contract_no)的来源之一，可用于发起代扣 / 订阅支付。

## 关键列
- `sign_contract_no`：签约协议号(协议号本体)，可作为 AUTODEBIT 等场景下的协议号来源使用。

## 主键/索引
原文未提供。

## 校验点(QA 关注)
- 协议号来源校验：测试 AUTODEBIT 等订阅 / 代扣场景时，可从 `t_contract_sign_info.sign_contract_no` 取协议号(另一来源为 PAYANDSIGN 后的 `t_deduct_protocol.deduct_protocol_no`)。
- 与 `tr_bank_card_token`(member 库，token=加密签约号) 配合，作为「卡是否已签约」及协议号取数的依据之一。
