---
id: scn_botim_vip_auto_sign_protocol
object_type: Scenario
name: Botim VIP 会员协议自动签署
aliases:
- VIP自动签约
- auto-sign protocol
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-25'
source_type: wiki_image
source_ref: wiki_image:a53d9f57-03c4-4403-9ecb-acb63d0f26c8
tags:
- Botim
- VIP
- 签约
- protocol
related_services:
- svc_protocol
- svc_member
related_tables: []
related_logs: []
---

# Botim VIP 会员协议自动签署

## 触发 / 入口

Botim 4.0.1 起，协议签署环节会自动识别 VIP 会员并默认完成签署，**跳过**常规手动签约流程。判定 + 处理在协议签署逻辑中触发。

## 关联关系

- **涉及服务**：[[svc_protocol]]（协议签署，`protocolService`）、[[svc_member]]（VIP 判定，`memberService`）（= `related_services`）
- **相关接口**：[[api_payby_apply_protocol]]（常规签约入口）

## 前置条件

- Botim 版本 ≥ 4.0.1。
- 当前会员可由 `memberService.isVipByMemberId(memberId)` 判定为 VIP。

## 操作步骤（逻辑分支）

1. 通过 `memberService.isVipByMemberId(domain.getMemberId())` 判断当前会员是否为 VIP。
2. 若为 VIP，调用 `protocolService.queryAndSignProtocol(...)` 自动完成协议签署。
3. 签署后直接 `return null`，短路后续协议签署相关逻辑。

`queryAndSignProtocol` 从 `domain` 对象取以下入参：
- `hostApp` = `domain.getHostApp()`
- `partnerId` = `domain.getPartnerId()`
- `identity` = `domain.getIdentity()`
- `memberId` = `domain.getMemberId()`
- `langType` = `domain.getLangType()`

## DB 校验点

- 待补：协议落库表（如 `t_contract_sign_info` / `t_deduct_protocol`）在自动签署后应生成对应记录（原文未明确指定校验表）。

## 预期结果

- 仅 VIP 会员走自动签署分支，非 VIP 会员仍按原流程手动签约。
- VIP 判定依据为 `memberId`，由 `memberService` 提供。
- 自动签署后返回 `null`，后续协议处理不再继续。
