---
id: svc_fundout
object_type: Service
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp012
name: fundout
aliases: [gp012_fundout]
related_services: [svc_member, svc_pbs, svc_pfs_payment, svc_acs, svc_css, svc_vis, svc_merchant, svc_voucher, svc_cards, svc_exchange]
related_tables: []
---

# fundout

> 作用与调用关系来自 **UAT Kibana trace 观测**(2026-06-22T20:00Z..06-23T01:00Z UAT cgs 回归窗口,真实但**非穷尽**——
> 未被该窗口触达的调用不会出现)。**候选,待人审**(核心原则 #2)。app_group=`gp012`。

## 作用
出款 / 代付核心 —— 编排 member/pbs/acs/css/vis/cards/merchant/voucher

## 下游调用（UAT trace 观测;observed_count=频次/权重）
| 被调服务 | 频次 | 置信 |
| --- | --- | ---: |
| member (`svc_member`) | 760 | high |
| pbs (`svc_pbs`) | 474 | high |
| pfs-payment (`svc_pfs_payment`) | 328 | high |
| acs (`svc_acs`) | 236 | high |
| css (`svc_css`) | 236 | high |
| vis (`svc_vis`) | 216 | high |
| merchant (`svc_merchant`) | 112 | high |
| voucher (`svc_voucher`) | 110 | high |
| cards (`svc_cards`) | 42 | high |
| exchange (`svc_exchange`) | 24 | high |

## 被调用方（←被调,本窗口观测）
merchant-fundout, merchant-frontend, personal, cashdesk-api

## 观测到的对外方法
createInnerFundout, createInnerFundoutV2

## 同组服务（app_group=gp012，共 1 个模块）
- （本组仅此一个）
