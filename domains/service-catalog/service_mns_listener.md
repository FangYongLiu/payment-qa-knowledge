---
id: svc_mns_listener
object_type: Service
domain: service-catalog
status: active
owner: unassigned
reviewer: unassigned
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp037
name: mns-listener
aliases: [gp037_mns-listener]
related_services: [svc_mns_main, svc_ues_ws]
related_tables: []
---

# mns-listener

> 作用与调用关系来自 **UAT Kibana trace 观测**(2026-06-22T20:00Z..06-23T01:00Z UAT cgs 回归窗口,真实但**非穷尽**——
> 未被该窗口触达的调用不会出现)。**候选,待人审**(核心原则 #2)。app_group=`gp037`。

## 作用
消息通知监听（MailNotify/SnsNotify，转 mns-main）

## 下游调用（UAT trace 观测;observed_count=频次/权重）
| 被调服务 | 频次 | 置信 |
| --- | --- | ---: |
| mns-main (`svc_mns_main`) | 3986 | med · **待核实** |
| ues-ws (`svc_ues_ws`) | 8 | med · **待核实** |

## 被调用方（←被调,本窗口观测）
(无)

## 观测到的对外方法
(无方法级证据)

## 同组服务（app_group=gp037，共 3 个模块）
- mns-main  (`svc_mns_main`)
- mns-scheduler  (`svc_mns_scheduler`)
