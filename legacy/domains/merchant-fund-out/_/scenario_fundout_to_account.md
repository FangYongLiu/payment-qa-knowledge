---
id: scn_fundout_to_account
object_type: Scenario
domain: fund-out-transfer
status: archived
owner: wiki-sync@acquire
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: wiki
source_ref: confluence:AQ/1012367385
tags:
- transfer
- SWIFT
- FEDWIRE
subdomain: null
module: null
sensitivity: normal
name: 商户出款到账户
aliases: []
related_services: []
related_tables: []
related_scenarios:
- scn_fundout_to_bankcard
related_logs: []
related_requirements: []
related_failures: []
---

## 触发/入口
- 产品集：Transfer to bank、Transfer To Bank Via SWIFT（通过 SWIFT 网络出款）、Transfer To Bank Via FEDWIRE（通过 FEDWIRE 网络出款）
- SGS 接口：transfer/placeTransferOrder
- 接口文档：https://developers.payby.com/docs/Transfer/
- 入口途径：商户控台

## 前置条件
- 商户已开通 Transfer 类产品集（含 SWIFT / FEDWIRE 对应权限）

## 操作步骤
1. 商户调用 SGS 接口 `transfer/placeTransferOrder` 发起出款到账户
2. 传入关键请求参数：
   - `amount.currency`：如 `AED`
   - `amount.amount`：如 `500`
   - `beneficiaryIdentity`：加密，如 `+971-585920614`
   - `beneficiaryIdentityType`：如 `PHONE_NO`

## DB 校验点
- `mhtfundout.t_fundout_account_order`：写入出款到账户订单记录

## 预期结果
- 通过 transfer/placeTransferOrder 成功创建出款到账户订单
- 资金按指定 currency/amount 出款给目标受益人（可通过 SWIFT 或 FEDWIRE 网络）
- 商户控台可查询到该笔出款到账户的订单
