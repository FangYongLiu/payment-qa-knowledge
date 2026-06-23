---
id: svc_offline_payment
object_type: Service
domain: service-catalog
status: active
owner: unassigned
reviewer: unassigned
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp308
name: offline-payment
aliases: [gp308_offline-payment]
related_services: [svc_pfs_payment, svc_member, svc_voucher, svc_pbs]
related_tables: []
---

# offline-payment

> 作用与调用关系来自 **UAT Kibana trace 观测**(2026-06-22T20:00Z..06-23T01:00Z UAT cgs 回归窗口,真实但**非穷尽**——
> 未被该窗口触达的调用不会出现)。**候选,待人审**(核心原则 #2)。app_group=`gp308`。

## 作用
线下支付（扫码 / POS 收款），编排 pfs/member/voucher/pbs

## 下游调用（UAT trace 观测;observed_count=频次/权重）
| 被调服务 | 频次 | 置信 |
| --- | --- | ---: |
| pfs-payment (`svc_pfs_payment`) | 13546 | high |
| member (`svc_member`) | 1304 | high |
| voucher (`svc_voucher`) | 648 | high |
| pbs (`svc_pbs`) | 339 | high |

## 被调用方（←被调,本窗口观测）
(无)

## 观测到的对外方法
(无方法级证据)

## 同组服务（app_group=gp308，共 1 个模块）
- （本组仅此一个）
