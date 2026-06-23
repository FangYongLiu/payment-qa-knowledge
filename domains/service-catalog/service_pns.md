---
id: svc_pns
object_type: Service
domain: service-catalog
status: active
owner: unassigned
reviewer: unassigned
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp013
name: pns
dev_owner: 刘智斌
aliases: [gp013_pns]
related_services: []
related_tables: []
---

# pns

> 作用与调用关系来自 **UAT Kibana trace 观测**(2026-06-22T20:00Z..06-23T01:00Z UAT cgs 回归窗口,真实但**非穷尽**——
> 未被该窗口触达的调用不会出现)。**候选,待人审**(核心原则 #2)。app_group=`gp013`。

## 作用
支付通知服务（notifyMerchant）—— 支付结果异步回调商户

## 下游调用（UAT trace 观测;observed_count=频次/权重）
(本窗口未观测到下游调用)

## 被调用方（←被调,本窗口观测）
merchant-frontend

## 观测到的对外方法
notifyMerchant

## 同组服务（app_group=gp013，共 1 个模块）
- （本组仅此一个）
