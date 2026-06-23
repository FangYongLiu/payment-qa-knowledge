---
id: svc_escrow
object_type: Service
domain: service-catalog
status: active
owner: unassigned
reviewer: unassigned
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp104
name: escrow
aliases: [gp104_escrow]
related_services: [svc_deposit, svc_voucher, svc_ues_ws, svc_ufs2]
related_tables: []
---

# escrow

> 作用与调用关系来自 **UAT Kibana trace 观测**(2026-06-22T20:00Z..06-23T01:00Z UAT cgs 回归窗口,真实但**非穷尽**——
> 未被该窗口触达的调用不会出现)。**候选,待人审**(核心原则 #2)。app_group=`gp104`。

## 作用
担保 / 托管交易（推断：调 deposit/voucher/ues）  **(待核实:仅凭调用关系推断,无方法证据)**

## 下游调用（UAT trace 观测;observed_count=频次/权重）
| 被调服务 | 频次 | 置信 |
| --- | --- | ---: |
| deposit (`svc_deposit`) | 350 | high |
| voucher (`svc_voucher`) | 280 | high |
| ues-ws (`svc_ues_ws`) | 245 | med · **待核实** |
| ufs2 (`svc_ufs2`) | 66 | med · **待核实** |

## 被调用方（←被调,本窗口观测）
(无)

## 观测到的对外方法
(无方法级证据)

## 同组服务（app_group=gp104，共 1 个模块）
- （本组仅此一个）
