---
id: flow_unionpay_card_issuance
object_type: Flow
domain: payby-core-systems
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-19'
source_type: wiki
source_ref: confluence:AQ/1268580390
tags:
- unionpay
- 开卡
- kyc
- escrow
- upic
subdomain: unionpay
module: card-issuance
sensitivity: normal
name: UnionPay开卡端到端流程
aliases: []
related_services: []
related_tables: []
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 概述
用户完成 KYC 后，由 escrow 系统向 upic 应用推送通知，upic 调用银联接口为用户开通银联卡，并将开卡记录落库。整个开卡过程对用户无感知（无声息），正常情况下不会失败，仅在网络异常时可能失败。

## 步骤(跨系统)
1. 用户完成 KYC。
2. escrow 系统向 upic 应用推送通知。
3. upic 接收到通知后，调用银联接口为用户开通银联卡。
4. 开卡成功后，将记录写入 `upic.t_upi_card`，状态为 `OS`。

## 涉及服务/表
- 服务：escrow（KYC 完成后推送通知）、upic（接收通知并调用银联接口开卡）
- 外部接口：银联开卡接口
- 表：`upic.t_upi_card`（开卡成功记录，状态 `OS`）

## 校验点
- 触发前提：用户已完成 KYC。
- 开卡成功后 `upic.t_upi_card` 中应存在记录，且状态为 `OS`。
- 用户无感知（无声息），无 UI 流程。
- 失败场景仅在网络异常时出现，正常情况不会失败。
- 开卡完成不等于可用，用户实际使用 UnionPay 功能前还需走激活流程（见 [[flow_unionpay_card_activation]]）。
