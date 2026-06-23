---
id: svc_reconciliation
object_type: Service
domain: service-catalog
status: active
owner: unassigned
reviewer: unassigned
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp043
name: reconciliation
aliases: [gp043_reconciliation]
related_services: [svc_dpm_manager, svc_member, svc_router, svc_cmf, svc_qpay_zand, svc_pfs_payment, svc_voucher]
related_tables: []
---

# reconciliation

> 作用与调用关系来自 **UAT Kibana trace 观测**(2026-06-22T20:00Z..06-23T01:00Z UAT cgs 回归窗口,真实但**非穷尽**——
> 未被该窗口触达的调用不会出现)。**候选,待人审**(核心原则 #2)。app_group=`gp043`。

## 作用
对账 —— 拉 dpm/member/router/cmf 数据核对

## 下游调用（UAT trace 观测;observed_count=频次/权重）
| 被调服务 | 频次 | 置信 |
| --- | --- | ---: |
| dpm-manager (`svc_dpm_manager`) | 10956 | high |
| member (`svc_member`) | 10782 | high |
| router (`svc_router`) | 9882 | high |
| cmf (`svc_cmf`) | 9491 | high |
| qpay-zand (`svc_qpay_zand`) | 2415 | high |
| pfs-payment (`svc_pfs_payment`) | 57 | high |
| voucher (`svc_voucher`) | 29 | high |

## 被调用方（←被调,本窗口观测）
remittance

## 观测到的对外方法
(无方法级证据)

## 同组服务（app_group=gp043，共 1 个模块）
- （本组仅此一个）
