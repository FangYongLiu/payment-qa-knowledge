---
id: svc_cashdesk_api
object_type: Service
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp007
name: cashdesk-api
dev_owner: 刘智斌
aliases: [gp007_cashdesk-api]
related_services: [svc_tradeii, svc_member, svc_grc_check_identity_provider, svc_protocol, svc_cmf, svc_authpay, svc_voucher, svc_ues_ws, svc_custom, svc_cards, svc_merchant, svc_fundout, svc_cms, svc_pbs, svc_marketing]
related_tables: []
---

# cashdesk-api

> 作用与调用关系来自 **UAT Kibana trace 观测**(2026-06-22T20:00Z..06-23T01:00Z UAT cgs 回归窗口,真实但**非穷尽**——
> 未被该窗口触达的调用不会出现)。**候选,待人审**(核心原则 #2)。app_group=`gp007`。

## 作用
统一收银台（Cashdesk）—— 收银台初始化 / 确认支付 / 协议签约 / 匿名卡支付（cardPayForAnonymous）

## 下游调用（UAT trace 观测;observed_count=频次/权重）
| 被调服务 | 频次 | 置信 |
| --- | --- | ---: |
| tradeii (`svc_tradeii`) | 648 | high |
| member (`svc_member`) | 592 | high |
| grc-check-identity-provider (`svc_grc_check_identity_provider`) | 280 | med · **待核实** |
| protocol (`svc_protocol`) | 208 | high |
| cmf (`svc_cmf`) | 166 | high |
| authpay (`svc_authpay`) | 150 | high |
| voucher (`svc_voucher`) | 114 | high |
| ues-ws (`svc_ues_ws`) | 112 | med · **待核实** |
| custom (`svc_custom`) | 80 | high |
| cards (`svc_cards`) | 74 | med · **待核实** |
| merchant (`svc_merchant`) | 56 | high |
| fundout (`svc_fundout`) | 48 | high |
| cms (`svc_cms`) | 16 | high |
| pbs (`svc_pbs`) | 16 | high |
| marketing (`svc_marketing`) | 15 | high |

## 被调用方（←被调,本窗口观测）
merchant-frontend, cmf, acquireii, cmf-task

## 观测到的对外方法
cardPayForAnonymous

## 同组服务（app_group=gp007，共 1 个模块）
- （本组仅此一个）
