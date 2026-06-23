---
id: svc_onboarding
object_type: Service
domain: service-catalog
status: active
owner: unassigned
reviewer: unassigned
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp254
name: onboarding
aliases: [gp254_onboarding]
related_services: []
related_tables: []
---

# onboarding

> 作用与调用关系来自 **UAT Kibana trace 观测**(2026-06-22T20:00Z..06-23T01:00Z UAT cgs 回归窗口,真实但**非穷尽**——
> 未被该窗口触达的调用不会出现)。**候选,待人审**(核心原则 #2)。app_group=`gp254`。

## 作用
商户 / 用户入网（被 router/qpay-mpgs 调用，加载商户 MerchantFacade）

## 下游调用（UAT trace 观测;observed_count=频次/权重）
(本窗口未观测到下游调用)

## 被调用方（←被调,本窗口观测）
router, qpay-mpgs

## 观测到的对外方法
(无方法级证据)

## 同组服务（app_group=gp254，共 1 个模块）
- （本组仅此一个）
