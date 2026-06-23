---
id: svc_rdgs
object_type: Service
domain: service-catalog
status: active
owner: unassigned
reviewer: unassigned
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp216
name: rdgs
dev_owner: 喻赛
aliases: [gp216_rdgs]
related_services: [svc_query, svc_ufs2]
related_tables: []
---

# rdgs

> 作用与调用关系来自 **UAT Kibana trace 观测**(2026-06-22T20:00Z..06-23T01:00Z UAT cgs 回归窗口,真实但**非穷尽**——
> 未被该窗口触达的调用不会出现)。**候选,待人审**(核心原则 #2)。app_group=`gp216`。

## 作用
报表 / 数据服务（调 query/ufs）

## 下游调用（UAT trace 观测;observed_count=频次/权重）
| 被调服务 | 频次 | 置信 |
| --- | --- | ---: |
| query (`svc_query`) | 92 | high |
| ufs2 (`svc_ufs2`) | 44 | med · **待核实** |

## 被调用方（←被调,本窗口观测）
(无)

## 观测到的对外方法
(无方法级证据)

## 同组服务（app_group=gp216，共 1 个模块）
- （本组仅此一个）
