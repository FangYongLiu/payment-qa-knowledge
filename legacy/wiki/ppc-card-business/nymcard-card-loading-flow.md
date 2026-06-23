---
title: NymCard卡片Loading充值流程时序
domain: ppc-card-business
kind: wiki_page
slug: nymcard-card-loading-flow
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:e558b9a8-3643-4d06-932f-45a1915290df
tags: []
---

# NymCard卡片Loading充值流程时序

本页描述持卡人发起 loading 后，由 Client 经 NymCard 到 PayBy 完成预付资金划拨与 credit 记账的两阶段时序。

## 参与方

- Cardholder：持卡人（发起方）
- Client：业务客户端/通道侧
- NymCard：发卡处理方
- PayBy：资金侧

## 阶段一：Loading 通道准备

- 1 `loading`：Cardholder → Client，发起充值请求
- 1.1 `loading channel process`：Client 内部自处理 loading 通道
- 1.2：Client 返回响应给 Cardholder

## 阶段二：实际 Load 与资金移动

- 2 `loading`：Client 内部再次自处理（进入第二阶段激活）
- 3 `load`：Client → NymCard，触发实际 load
- 3.1 `move pre funds`：NymCard → PayBy，移动预付资金
- 3.2 `success`：PayBy → NymCard，返回成功
- 3.3 `do credit`：NymCard 内部执行 credit 记账
- 3.4：NymCard 返回 Client

## 关键说明

- 整个流程分为两次 Client 激活：第一次完成 loading 通道处理并回包给 Cardholder；第二次驱动真实的资金移动与记账。
- 资金路径：Client → NymCard → PayBy（`move pre funds`），成功后由 NymCard 完成 `do credit`。
- credit 记账发生在 PayBy 返回 `success` 之后，由 NymCard 自身完成。
