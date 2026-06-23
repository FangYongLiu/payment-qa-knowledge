---
id: svc_router
object_type: Service
domain: service-catalog
status: active
owner: unassigned
reviewer: unassigned
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp124
name: router
aliases: [gp124_router]
related_services: [svc_onboarding, svc_cmf]
related_tables: []
---

# router

> 作用与调用关系来自 **UAT Kibana trace 观测**(2026-06-22T20:00Z..06-23T01:00Z UAT cgs 回归窗口,真实但**非穷尽**——
> 未被该窗口触达的调用不会出现)。**候选,待人审**(核心原则 #2)。app_group=`gp124`。

## 作用
渠道路由（Channel Router）—— 按 apiType 选可用渠道（queryChannelArchive/getChannelsByApiTypes），下游 onboarding/cmf

## 下游调用（UAT trace 观测;observed_count=频次/权重）
| 被调服务 | 频次 | 置信 |
| --- | --- | ---: |
| onboarding (`svc_onboarding`) | 4852 | high |
| cmf (`svc_cmf`) | 706 | high |

## 被调用方（←被调,本窗口观测）
remittance, cmf, cmf-task, reconciliation, cregister

## 观测到的对外方法
(无方法级证据)

## 同组服务（app_group=gp124，共 1 个模块）
- （本组仅此一个）
