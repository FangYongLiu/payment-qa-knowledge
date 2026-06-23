---
id: svc_merchant_console_frontend
object_type: Service
domain: service-catalog
status: active
owner: unassigned
reviewer: unassigned
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp045
name: merchant-console-frontend
aliases: [gp045_merchant-console-frontend]
related_services: [svc_member, svc_merchant, svc_grc_check_identity_provider]
related_tables: []
---

# merchant-console-frontend

> 作用与调用关系来自 **UAT Kibana trace 观测**(2026-06-22T20:00Z..06-23T01:00Z UAT cgs 回归窗口,真实但**非穷尽**——
> 未被该窗口触达的调用不会出现)。**候选,待人审**(核心原则 #2)。app_group=`gp045`。

## 作用
商户控制台前端 BFF（商户后台操作入口）

## 下游调用（UAT trace 观测;observed_count=频次/权重）
| 被调服务 | 频次 | 置信 |
| --- | --- | ---: |
| member (`svc_member`) | 27 | high |
| merchant (`svc_merchant`) | 9 | high |
| grc-check-identity-provider (`svc_grc_check_identity_provider`) | 3 | med · **待核实** |

## 被调用方（←被调,本窗口观测）
(无)

## 观测到的对外方法
(无方法级证据)

## 同组服务（app_group=gp045，共 1 个模块）
- （本组仅此一个）
