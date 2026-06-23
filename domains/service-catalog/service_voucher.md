---
id: svc_voucher
object_type: Service
domain: service-catalog
status: active
owner: unassigned
reviewer: unassigned
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp009
name: voucher
aliases: [gp009_voucher]
related_services: []
related_tables: []
---

# voucher

> 作用与调用关系来自 **UAT Kibana trace 观测**(2026-06-22T20:00Z..06-23T01:00Z UAT cgs 回归窗口,真实但**非穷尽**——
> 未被该窗口触达的调用不会出现)。**候选,待人审**(核心原则 #2)。app_group=`gp009`。

## 作用
全局 ID 与幂等凭证（getGlobalId / recordReqVoucher）—— 被交易 / 收单 / 出款广泛调用的基础设施

## 下游调用（UAT trace 观测;observed_count=频次/权重）
(本窗口未观测到下游调用)

## 被调用方（←被调,本窗口观测）
tradeii, vis, offline-payment, acquireii, escrow, merchant-fundout

## 观测到的对外方法
getGlobalId, recordReqVoucher

## 同组服务（app_group=gp009，共 1 个模块）
- （本组仅此一个）
