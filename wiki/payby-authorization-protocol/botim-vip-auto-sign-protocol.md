---
title: Botim VIP会员协议自动签署逻辑
domain: payby-authorization-protocol
kind: wiki_page
slug: botim-vip-auto-sign-protocol
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:a53d9f57-03c4-4403-9ecb-acb63d0f26c8
tags: []
---

# Botim VIP会员协议自动签署逻辑

在 Botim 4.0.1 中，VIP 会员在协议签署环节会被自动识别并默认完成签署，跳过常规的手动签约流程。

## 判断与处理流程

1. 通过 `memberService.isVipByMemberId(domain.getMemberId())` 判断当前会员是否为 VIP。
2. 若为 VIP，则调用 `protocolService.queryAndSignProtocol(...)` 自动完成协议签署。
3. 签署后直接 `return null`，短路后续协议签署相关逻辑。

## queryAndSignProtocol 入参

调用 `protocolService.queryAndSignProtocol` 时，从 `domain` 对象中取以下参数：

- `hostApp` — `domain.getHostApp()`
- `partnerId` — `domain.getPartnerId()`
- `identity` — `domain.getIdentity()`
- `memberId` — `domain.getMemberId()`
- `langType` — `domain.getLangType()`

## 关键说明

- 仅 VIP 会员走该自动签署分支，非 VIP 会员仍按原流程处理。
- VIP 判定依据为 `memberId`，由 `memberService` 提供。
- 自动签署后返回 `null`，表示后续协议处理不再继续。
