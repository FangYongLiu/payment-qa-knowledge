---
id: svc_cashierii
object_type: Service
domain: service-catalog
status: active
owner: unassigned
reviewer: unassigned
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp193
name: cashierii
aliases: [gp193_cashierii]
related_services: [svc_tradeii, svc_member, svc_grc_check_identity_provider, svc_merchant, svc_authpay, svc_cmf, svc_mns_main, svc_cards, svc_voucher, svc_protocol, svc_cmsii, svc_member_front, svc_pbs, svc_qpay_lean]
related_tables: []
---

# cashierii

> 作用与调用关系来自 **UAT Kibana trace 观测**(2026-06-22T20:00Z..06-23T01:00Z UAT cgs 回归窗口,真实但**非穷尽**——
> 未被该窗口触达的调用不会出现)。**候选,待人审**(核心原则 #2)。app_group=`gp193`。

## 作用
收银核心（Cashier II）—— 下单 / 确认支付 / 查支付结果（queryPosPayResult），编排 tradeii/member/grc/authpay/cards

## 下游调用（UAT trace 观测;observed_count=频次/权重）
| 被调服务 | 频次 | 置信 |
| --- | --- | ---: |
| tradeii (`svc_tradeii`) | 767 | high |
| member (`svc_member`) | 527 | high |
| grc-check-identity-provider (`svc_grc_check_identity_provider`) | 282 | med · **待核实** |
| merchant (`svc_merchant`) | 163 | high |
| authpay (`svc_authpay`) | 160 | high |
| cmf (`svc_cmf`) | 112 | high |
| mns-main (`svc_mns_main`) | 91 | med · **待核实** |
| cards (`svc_cards`) | 88 | high |
| voucher (`svc_voucher`) | 76 | high |
| protocol (`svc_protocol`) | 56 | high |
| cmsii (`svc_cmsii`) | 46 | high |
| member-front (`svc_member_front`) | 40 | high |
| pbs (`svc_pbs`) | 32 | high |
| qpay-lean (`svc_qpay_lean`) | 14 | med · **待核实** |

## 被调用方（←被调,本窗口观测）
tradeii, acquireii

## 观测到的对外方法
queryPosPayResult

## 同组服务（app_group=gp193，共 1 个模块）
- （本组仅此一个）
