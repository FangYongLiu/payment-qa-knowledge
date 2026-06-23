---
id: svc_cmf
object_type: Service
domain: payment-tools
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp002
name: cmf
dev_owner: 张鹤飞
aliases: [gp002_cmf]
related_services: [svc_router, svc_member, svc_grc_check_identity_provider, svc_cashdesk_api, svc_exchange, svc_ues_ws]
related_tables: []
---

# cmf

> 作用与调用关系来自 **UAT Kibana trace 观测**(2026-06-22T20:00Z..06-23T01:00Z UAT cgs 回归窗口,真实但**非穷尽**——
> 未被该窗口触达的调用不会出现)。**候选,待人审**(核心原则 #2)。app_group=`gp002`。

## 作用
渠道管理与资金（Channel Mgmt & Fund）—— 经 router 选渠道，连 member/exchange/cashdesk，被 payment/trade/reconciliation/fcw 等广泛调用

## 下游调用（UAT trace 观测;observed_count=频次/权重）
| 被调服务 | 频次 | 置信 |
| --- | --- | ---: |
| router (`svc_router`) | 45109 | high |
| member (`svc_member`) | 396 | high |
| grc-check-identity-provider (`svc_grc_check_identity_provider`) | 197 | med · **待核实** |
| cashdesk-api (`svc_cashdesk_api`) | 50 | high |
| exchange (`svc_exchange`) | 47 | med · **待核实** |
| ues-ws (`svc_ues_ws`) | 45 | med · **待核实** |

## 被调用方（←被调,本窗口观测）
reconciliation, tradeii, payment, router, fcw, cashdesk-api

## 观测到的对外方法
(无方法级证据)

## 同组服务（app_group=gp002，共 2 个模块）
- cmf-task  (`svc_cmf_task`)
