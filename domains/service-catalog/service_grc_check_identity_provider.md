---
id: svc_grc_check_identity_provider
object_type: Service
domain: service-catalog
status: active
owner: unassigned
reviewer: unassigned
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp079
name: grc-check-identity-provider
aliases: [gp079_grc-check-identity-provider]
related_services: [svc_member]
related_tables: []
---

# grc-check-identity-provider

> 作用与调用关系来自 **UAT Kibana trace 观测**(2026-06-22T20:00Z..06-23T01:00Z UAT cgs 回归窗口,真实但**非穷尽**——
> 未被该窗口触达的调用不会出现)。**候选,待人审**(核心原则 #2)。app_group=`gp079`。

## 作用
风控合规身份校验（GRC）—— 被 cashier/cashdesk/cmf/aml 调用做风险事件 / 身份校验

## 下游调用（UAT trace 观测;observed_count=频次/权重）
| 被调服务 | 频次 | 置信 |
| --- | --- | ---: |
| member (`svc_member`) | 162 | high |

## 被调用方（←被调,本窗口观测）
cashierii, cashdesk-api, cmf, aml, qpay-mpgs, remittance

## 观测到的对外方法
(无方法级证据)

## 同组服务（app_group=gp079，共 4 个模块）
- grc-component-connect-provider  (`svc_grc_component_connect_provider`)
- grc-cps-provider  (`svc_grc_cps_provider`)
- grc-engine-provider  (`svc_grc_engine_provider`)
