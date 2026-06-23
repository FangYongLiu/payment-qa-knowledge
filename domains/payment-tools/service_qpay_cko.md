---
id: svc_qpay_cko
object_type: Service
domain: payment-tools
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp221
name: qpay-cko
aliases: [gp221_qpay-cko]
related_services: [svc_cards, svc_grc_check_identity_provider]
related_tables: []
---

# qpay-cko

> 作用与调用关系来自 **UAT Kibana trace 观测**(2026-06-22T20:00Z..06-23T01:00Z UAT cgs 回归窗口,真实但**非穷尽**——
> 未被该窗口触达的调用不会出现)。**候选,待人审**(核心原则 #2)。app_group=`gp221`。

## 作用
Checkout.com（CKO）渠道接入

## 下游调用（UAT trace 观测;observed_count=频次/权重）
| 被调服务 | 频次 | 置信 |
| --- | --- | ---: |
| cards (`svc_cards`) | 12 | high |
| grc-check-identity-provider (`svc_grc_check_identity_provider`) | 12 | med · **待核实** |

## 被调用方（←被调,本窗口观测）
(无)

## 观测到的对外方法
(无方法级证据)

## 同组服务（app_group=gp221，共 1 个模块）
- （本组仅此一个）
