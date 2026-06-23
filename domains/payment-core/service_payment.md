---
id: svc_payment
object_type: Service
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp006
name: payment
dev_owner: 李德文
aliases: [gp006_payment]
related_services: [svc_dpm_manager, svc_cmf, svc_pfs_payment, svc_counter, svc_member]
related_tables: []
---

# payment

> 作用与调用关系来自 **UAT Kibana trace 观测**(2026-06-22T20:00Z..06-23T01:00Z UAT cgs 回归窗口,真实但**非穷尽**——
> 未被该窗口触达的调用不会出现)。**候选,待人审**(核心原则 #2)。app_group=`gp006`。

## 作用
支付中台 —— 支付指令处理，编排 dpm（记账）/cmf（渠道）/pfs（履约）/counter

## 下游调用（UAT trace 观测;observed_count=频次/权重）
| 被调服务 | 频次 | 置信 |
| --- | --- | ---: |
| dpm-manager (`svc_dpm_manager`) | 2653 | high |
| cmf (`svc_cmf`) | 999 | high |
| pfs-payment (`svc_pfs_payment`) | 536 | high |
| counter (`svc_counter`) | 456 | high |
| member (`svc_member`) | 78 | med · **待核实** |

## 被调用方（←被调,本窗口观测）
pfs-payment

## 观测到的对外方法
(无方法级证据)

## 同组服务（app_group=gp006，共 1 个模块）
- （本组仅此一个）
