---
id: svc_merchant
object_type: Service
domain: service-catalog
status: active
owner: unassigned
reviewer: unassigned
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp044
name: merchant
aliases: [gp044_merchant]
related_services: [svc_aml, svc_authorization_service]
related_tables: []
---

# merchant

> 作用与调用关系来自 **UAT Kibana trace 观测**(2026-06-22T20:00Z..06-23T01:00Z UAT cgs 回归窗口,真实但**非穷尽**——
> 未被该窗口触达的调用不会出现)。**候选,待人审**(核心原则 #2)。app_group=`gp044`。

## 作用
商户主数据 / 商户管理（queryStaffPage/getStaff、ProductAudit、Aml）—— 被收单 / 收银 / 出款调用

## 下游调用（UAT trace 观测;observed_count=频次/权重）
| 被调服务 | 频次 | 置信 |
| --- | --- | ---: |
| aml (`svc_aml`) | 12335 | high |
| authorization-service (`svc_authorization_service`) | 20 | med · **待核实** |

## 被调用方（←被调,本窗口观测）
merchant-frontend, merchant-fundout, cashierii, mssii, fundout, device

## 观测到的对外方法
queryStaffPage, getStaff

## 同组服务（app_group=gp044，共 1 个模块）
- （本组仅此一个）
