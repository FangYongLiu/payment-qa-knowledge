---
id: svc_remittance
object_type: Service
domain: service-catalog
status: active
owner: unassigned
reviewer: unassigned
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp188
name: remittance
aliases: [gp188_remittance]
related_services: [svc_member, svc_router, svc_acs, svc_tradeii, svc_cms, svc_reconciliation, svc_voucher, svc_grc_check_identity_provider, svc_aml]
related_tables: []
---

# remittance

> 作用与调用关系来自 **UAT Kibana trace 观测**(2026-06-22T20:00Z..06-23T01:00Z UAT cgs 回归窗口,真实但**非穷尽**——
> 未被该窗口触达的调用不会出现)。**候选,待人审**(核心原则 #2)。app_group=`gp188`。

## 作用
跨境汇款核心 —— 编排 member/router/acs/tradeii/reconciliation + 各汇款渠道（terrapay/arp/fuze）

## 下游调用（UAT trace 观测;observed_count=频次/权重）
| 被调服务 | 频次 | 置信 |
| --- | --- | ---: |
| member (`svc_member`) | 64072 | high |
| router (`svc_router`) | 52455 | high |
| acs (`svc_acs`) | 118 | high |
| tradeii (`svc_tradeii`) | 105 | high |
| cms (`svc_cms`) | 56 | high |
| reconciliation (`svc_reconciliation`) | 42 | high |
| voucher (`svc_voucher`) | 42 | high |
| grc-check-identity-provider (`svc_grc_check_identity_provider`) | 35 | med · **待核实** |
| aml (`svc_aml`) | 18 | high |

## 被调用方（←被调,本窗口观测）
fcw

## 观测到的对外方法
(无方法级证据)

## 同组服务（app_group=gp188，共 1 个模块）
- （本组仅此一个）
