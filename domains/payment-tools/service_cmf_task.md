---
id: svc_cmf_task
object_type: Service
domain: payment-tools
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp002
name: cmf-task
aliases: [gp002_cmf-task]
related_services: [svc_router, svc_exchange, svc_ues_ws, svc_cashdesk_api]
related_tables: []
---

# cmf-task

> 作用与调用关系来自 **UAT Kibana trace 观测**(2026-06-22T20:00Z..06-23T01:00Z UAT cgs 回归窗口,真实但**非穷尽**——
> 未被该窗口触达的调用不会出现)。**候选,待人审**(核心原则 #2)。app_group=`gp002`。

## 作用
cmf 异步任务（定时 / 后台渠道处理）

## 下游调用（UAT trace 观测;observed_count=频次/权重）
| 被调服务 | 频次 | 置信 |
| --- | --- | ---: |
| router (`svc_router`) | 13198 | high |
| exchange (`svc_exchange`) | 18 | med · **待核实** |
| ues-ws (`svc_ues_ws`) | 12 | med · **待核实** |
| cashdesk-api (`svc_cashdesk_api`) | 4 | high |

## 被调用方（←被调,本窗口观测）
(无)

## 观测到的对外方法
(无方法级证据)

## 同组服务（app_group=gp002，共 2 个模块）
- cmf  (`svc_cmf`)
