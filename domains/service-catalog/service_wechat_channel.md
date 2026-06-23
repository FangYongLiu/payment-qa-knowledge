---
id: svc_wechat_channel
object_type: Service
domain: service-catalog
status: active
owner: unassigned
reviewer: unassigned
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp236
name: wechat-channel
aliases: [gp236_wechat-channel]
related_services: [svc_acs, svc_ues_ws]
related_tables: []
---

# wechat-channel

> 作用与调用关系来自 **UAT Kibana trace 观测**(2026-06-22T20:00Z..06-23T01:00Z UAT cgs 回归窗口,真实但**非穷尽**——
> 未被该窗口触达的调用不会出现)。**候选,待人审**(核心原则 #2)。app_group=`gp236`。

## 作用
微信支付渠道接入，调 acs 风控 / ues 用户数据

## 下游调用（UAT trace 观测;observed_count=频次/权重）
| 被调服务 | 频次 | 置信 |
| --- | --- | ---: |
| acs (`svc_acs`) | 31318 | high |
| ues-ws (`svc_ues_ws`) | 7830 | med · **待核实** |

## 被调用方（←被调,本窗口观测）
(无)

## 观测到的对外方法
(无方法级证据)

## 同组服务（app_group=gp236，共 1 个模块）
- （本组仅此一个）
