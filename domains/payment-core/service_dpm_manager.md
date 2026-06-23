---
id: svc_dpm_manager
object_type: Service
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp004
name: dpm-manager
dev_owner: 周聪
aliases: [gp004_dpm-manager]
related_services: []
related_tables: []
---

# dpm-manager

> 作用与调用关系来自 **UAT Kibana trace 观测**(2026-06-22T20:00Z..06-23T01:00Z UAT cgs 回归窗口,真实但**非穷尽**——
> 未被该窗口触达的调用不会出现)。**候选,待人审**(核心原则 #2)。app_group=`gp004`。

## 作用
账务平台管理（DPM）—— 记账主入口，被 pfs/payment/reconciliation 调用

## 下游调用（UAT trace 观测;observed_count=频次/权重）
(本窗口未观测到下游调用)

## 被调用方（←被调,本窗口观测）
pfs-payment, reconciliation, payment

## 观测到的对外方法
(无方法级证据)

## 同组服务（app_group=gp004，共 3 个模块）
- dpm-accounting  (`svc_dpm_accounting`)
- dpm-task  (`svc_dpm_task`)
