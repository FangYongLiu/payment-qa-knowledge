---
id: svc_acquireii
object_type: Service
domain: service-catalog
status: active
owner: unassigned
reviewer: unassigned
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp069
name: acquireii
aliases: [gp069_acquireii]
related_services: [svc_tradeii, svc_voucher, svc_ppcenter, svc_ues_ws, svc_marketing, svc_member, svc_cmf, svc_device, svc_cashdesk_api, svc_cashierii]
related_tables: []
---

# acquireii

> 作用与调用关系来自 **UAT Kibana trace 观测**(2026-06-22T20:00Z..06-23T01:00Z UAT cgs 回归窗口,真实但**非穷尽**——
> 未被该窗口触达的调用不会出现)。**候选,待人审**(核心原则 #2)。app_group=`gp069`。

## 作用
收单核心（Acquire II）—— 商户订单受理 / 下单 / 退款受理，编排 tradeii、voucher、ppcenter、marketing、member

## 下游调用（UAT trace 观测;observed_count=频次/权重）
| 被调服务 | 频次 | 置信 |
| --- | --- | ---: |
| tradeii (`svc_tradeii`) | 958 | high |
| voucher (`svc_voucher`) | 349 | high |
| ppcenter (`svc_ppcenter`) | 275 | high |
| ues-ws (`svc_ues_ws`) | 176 | med · **待核实** |
| marketing (`svc_marketing`) | 136 | high |
| member (`svc_member`) | 131 | high |
| cmf (`svc_cmf`) | 24 | high |
| device (`svc_device`) | 21 | high |
| cashdesk-api (`svc_cashdesk_api`) | 6 | high |
| cashierii (`svc_cashierii`) | 1 | high |

## 被调用方（←被调,本窗口观测）
merchant-frontend

## 观测到的对外方法
(无方法级证据)

## 同组服务（app_group=gp069，共 1 个模块）
- （本组仅此一个）
