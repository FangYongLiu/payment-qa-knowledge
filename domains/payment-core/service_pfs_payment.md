---
id: svc_pfs_payment
object_type: Service
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp014
name: pfs-payment
dev_owner: 李德文
aliases: [gp014_pfs-payment]
related_services: [svc_member, svc_payment, svc_dpm_manager]
related_tables: []
---

# pfs-payment

> 作用与调用关系来自 **UAT Kibana trace 观测**(2026-06-22T20:00Z..06-23T01:00Z UAT cgs 回归窗口,真实但**非穷尽**——
> 未被该窗口触达的调用不会出现)。**候选,待人审**(核心原则 #2)。app_group=`gp014`。

## 作用
支付履约 / 清分（Payment Fulfillment，enterMulti），被 trade/payment/offline/vis 调用

## 下游调用（UAT trace 观测;observed_count=频次/权重）
| 被调服务 | 频次 | 置信 |
| --- | --- | ---: |
| member (`svc_member`) | 20798 | med · **待核实** |
| payment (`svc_payment`) | 20583 | high |
| dpm-manager (`svc_dpm_manager`) | 19978 | high |

## 被调用方（←被调,本窗口观测）
offline-payment, vis, payment, tradeii, fundout, reconciliation

## 观测到的对外方法
enterMulti

## 同组服务（app_group=gp014，共 3 个模块）
- pfs-basis  (`svc_pfs_basis`)
- pfs-manager  (`svc_pfs_manager`)
