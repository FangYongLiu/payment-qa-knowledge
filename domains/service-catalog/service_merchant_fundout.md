---
id: svc_merchant_fundout
object_type: Service
domain: service-catalog
status: active
owner: unassigned
reviewer: unassigned
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp083
name: merchant-fundout
aliases: [gp083_merchant-fundout]
related_services: [svc_fundout, svc_merchant, svc_voucher, svc_member, svc_ppcenter, svc_tradeii, svc_ues_ws]
related_tables: []
---

# merchant-fundout

> 作用与调用关系来自 **UAT Kibana trace 观测**(2026-06-22T20:00Z..06-23T01:00Z UAT cgs 回归窗口,真实但**非穷尽**——
> 未被该窗口触达的调用不会出现)。**候选,待人审**(核心原则 #2)。app_group=`gp083`。

## 作用
商户出款 / 结算代付，调 merchant/fundout(Fos)/voucher/ppcenter

## 下游调用（UAT trace 观测;observed_count=频次/权重）
| 被调服务 | 频次 | 置信 |
| --- | --- | ---: |
| fundout (`svc_fundout`) | 1825 | med · **待核实** |
| merchant (`svc_merchant`) | 246 | high |
| voucher (`svc_voucher`) | 218 | high |
| member (`svc_member`) | 108 | high |
| ppcenter (`svc_ppcenter`) | 80 | high |
| tradeii (`svc_tradeii`) | 24 | high |
| ues-ws (`svc_ues_ws`) | 14 | med · **待核实** |

## 被调用方（←被调,本窗口观测）
(无)

## 观测到的对外方法
(无方法级证据)

## 同组服务（app_group=gp083，共 1 个模块）
- （本组仅此一个）
