---
id: svc_device
object_type: Service
domain: service-catalog
status: active
owner: unassigned
reviewer: unassigned
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp054
name: device
aliases: [gp054_device]
related_services: [svc_ppcenter, svc_merchant]
related_tables: []
---

# device

> 作用与调用关系来自 **UAT Kibana trace 观测**(2026-06-22T20:00Z..06-23T01:00Z UAT cgs 回归窗口,真实但**非穷尽**——
> 未被该窗口触达的调用不会出现)。**候选,待人审**(核心原则 #2)。app_group=`gp054`。

## 作用
设备 / 产品中心接入（调 ppcenter/merchant/store）

## 下游调用（UAT trace 观测;observed_count=频次/权重）
| 被调服务 | 频次 | 置信 |
| --- | --- | ---: |
| ppcenter (`svc_ppcenter`) | 3600 | high |
| merchant (`svc_merchant`) | 108 | high |

## 被调用方（←被调,本窗口观测）
acquireii

## 观测到的对外方法
(无方法级证据)

## 同组服务（app_group=gp054，共 1 个模块）
- （本组仅此一个）
