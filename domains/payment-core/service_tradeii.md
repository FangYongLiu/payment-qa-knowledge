---
id: svc_tradeii
object_type: Service
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp123
name: tradeii
dev_owner: 唐宇
aliases: [gp123_tradeii]
related_services: [svc_voucher, svc_member, svc_cmf, svc_pfs_payment, svc_pbs, svc_acs, svc_cards, svc_css, svc_cashierii, svc_authpay, svc_cms, svc_deduct]
related_tables: []
---

# tradeii

> 作用与调用关系来自 **UAT Kibana trace 观测**(2026-06-22T20:00Z..06-23T01:00Z UAT cgs 回归窗口,真实但**非穷尽**——
> 未被该窗口触达的调用不会出现)。**候选,待人审**(核心原则 #2)。app_group=`gp123`。

## 作用
交易订单引擎（Trade II）—— 创建 / 查询交易、退款、收银交易（queryTradeOrder/createCashierTrade/refund），编排 voucher/cmf/pbs/acs/cards/cashier/pfs

## 下游调用（UAT trace 观测;observed_count=频次/权重）
| 被调服务 | 频次 | 置信 |
| --- | --- | ---: |
| voucher (`svc_voucher`) | 11646 | high |
| member (`svc_member`) | 1595 | high |
| cmf (`svc_cmf`) | 1505 | high |
| pfs-payment (`svc_pfs_payment`) | 520 | high |
| pbs (`svc_pbs`) | 192 | high |
| acs (`svc_acs`) | 190 | high |
| cards (`svc_cards`) | 150 | high |
| css (`svc_css`) | 117 | high |
| cashierii (`svc_cashierii`) | 114 | high |
| authpay (`svc_authpay`) | 21 | high |
| cms (`svc_cms`) | 21 | high |
| deduct (`svc_deduct`) | 14 | high |

## 被调用方（←被调,本窗口观测）
acquireii, cashierii, cashdesk-api, remittance, merchant-fundout, deduct

## 观测到的对外方法
queryTradeOrder, queryRefundOrder, createCashierTrade, refund

## 同组服务（app_group=gp123，共 1 个模块）
- （本组仅此一个）
