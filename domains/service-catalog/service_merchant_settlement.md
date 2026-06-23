---
id: svc_merchant_settlement
object_type: Service
domain: service-catalog
status: active
owner: unassigned
reviewer: unassigned
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp288
name: merchant-settlement
aliases: [gp288_merchant-settlement]
related_services: []
related_tables: []
---

# merchant-settlement

> 作用与调用关系来自 **UAT Kibana trace 观测**(2026-06-22T20:00Z..06-23T01:00Z UAT cgs 回归窗口,真实但**非穷尽**——
> 未被该窗口触达的调用不会出现)。**候选,待人审**(核心原则 #2)。app_group=`gp288`。

## 作用
商户结算（被 statementii 调用，推断）  **(待核实:仅凭调用关系推断,无方法证据)**

## 下游调用（UAT trace 观测;observed_count=频次/权重）
(本窗口未观测到下游调用)

## 被调用方（←被调,本窗口观测）
statementii

## 观测到的对外方法
(无方法级证据)

## 同组服务（app_group=gp288，共 1 个模块）
- （本组仅此一个）
