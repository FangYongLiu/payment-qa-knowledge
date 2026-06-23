---
id: svc_acs
object_type: Service
domain: risk
status: active
owner: xinwei.cao,dewen.li
reviewer: xinwei.cao,dewen.li
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp008
name: acs
dev_owner: 喻赛
aliases: [gp008_acs]
related_services: []
related_tables: []
---

# acs

> 作用与调用关系来自 **UAT Kibana trace 观测**(2026-06-22T20:00Z..06-23T01:00Z UAT cgs 回归窗口,真实但**非穷尽**——
> 未被该窗口触达的调用不会出现)。**候选,待人审**(核心原则 #2)。app_group=`gp008`。

## 作用
反欺诈 / 风控 + 渠道密钥（ACS，queryPartnerKey）—— 被渠道 / 收单 / 出款 / 汇款广泛调用

## 下游调用（UAT trace 观测;observed_count=频次/权重）
(本窗口未观测到下游调用)

## 被调用方（←被调,本窗口观测）
wechat-channel, pbs, iso8583-gateway, fundout, tradeii, marketing-event

## 观测到的对外方法
queryPartnerKey

## 同组服务（app_group=gp008，共 1 个模块）
- （本组仅此一个）
