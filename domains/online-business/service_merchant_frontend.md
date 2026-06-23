---
id: svc_merchant_frontend
object_type: Service
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp071
name: merchant-frontend
dev_owner: 王斌
aliases: [gp071_merchant-frontend]
related_services: [svc_acquireii, svc_merchant, svc_pns, svc_ues_ws, svc_cards, svc_member, svc_fundout, svc_cashdesk_api, svc_statementii, svc_voucher, svc_kyc, svc_cmf, svc_acs]
related_tables: []
---

# merchant-frontend

> 作用与调用关系来自 **UAT Kibana trace 观测**(2026-06-22T20:00Z..06-23T01:00Z UAT cgs 回归窗口,真实但**非穷尽**——
> 未被该窗口触达的调用不会出现)。**候选,待人审**(核心原则 #2)。app_group=`gp071`。

## 作用
SGS 收单网关 / 商户侧支付 BFF —— 商户 acquire 类 API 的入口，转发到 acquireii，并直连 merchant/pns/cards/cashdesk

## 下游调用（UAT trace 观测;observed_count=频次/权重）
| 被调服务 | 频次 | 置信 |
| --- | --- | ---: |
| acquireii (`svc_acquireii`) | 322488 | high |
| merchant (`svc_merchant`) | 209679 | high |
| pns (`svc_pns`) | 16832 | high |
| ues-ws (`svc_ues_ws`) | 5594 | med · **待核实** |
| cards (`svc_cards`) | 4011 | high |
| member (`svc_member`) | 2190 | high |
| fundout (`svc_fundout`) | 1363 | high |
| cashdesk-api (`svc_cashdesk_api`) | 906 | high |
| statementii (`svc_statementii`) | 453 | high |
| voucher (`svc_voucher`) | 20 | high |
| kyc (`svc_kyc`) | 4 | high |
| cmf (`svc_cmf`) | 2 | med · **待核实** |
| acs (`svc_acs`) | 1 | high |

## 被调用方（←被调,本窗口观测）
(无)

## 观测到的对外方法
(无方法级证据)

## 同组服务（app_group=gp071，共 1 个模块）
- （本组仅此一个）
