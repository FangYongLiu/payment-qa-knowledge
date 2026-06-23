---
id: svc_deduct
object_type: Service
domain: service-catalog
status: active
owner: unassigned
reviewer: unassigned
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp205
name: deduct
aliases: [gp205_deduct]
related_services: [svc_protocol, svc_tradeii]
related_tables: []
---

# deduct

> 作用与调用关系来自 **UAT Kibana trace 观测**(2026-06-22T20:00Z..06-23T01:00Z UAT cgs 回归窗口,真实但**非穷尽**——
> 未被该窗口触达的调用不会出现)。**候选,待人审**(核心原则 #2)。app_group=`gp205`。

## 作用
自动代扣执行（queryProtocol，调 protocol/trade）

## 下游调用（UAT trace 观测;observed_count=频次/权重）
| 被调服务 | 频次 | 置信 |
| --- | --- | ---: |
| protocol (`svc_protocol`) | 32 | high |
| tradeii (`svc_tradeii`) | 15 | high |

## 被调用方（←被调,本窗口观测）
tradeii

## 观测到的对外方法
queryProtocol

## 同组服务（app_group=gp205，共 1 个模块）
- （本组仅此一个）
