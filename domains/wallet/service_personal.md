---
id: svc_personal
object_type: Service
domain: wallet
status: active
owner: qianlong.wang
reviewer: qianlong.wang
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp032
name: personal
dev_owner: 刘智斌
aliases: [gp032_personal]
related_services: [svc_member, svc_pts, svc_fundout, svc_acs, svc_cmf]
related_tables: []
---

# personal

> 作用与调用关系来自 **UAT Kibana trace 观测**(2026-06-22T20:00Z..06-23T01:00Z UAT cgs 回归窗口,真实但**非穷尽**——
> 未被该窗口触达的调用不会出现)。**候选,待人审**(核心原则 #2)。app_group=`gp032`。

## 作用
个人（C 端）账户服务 —— 登录 / 绑卡 / 转账 / 提现入口，调 member(Ma)/pts/acs/cmf

## 下游调用（UAT trace 观测;observed_count=频次/权重）
| 被调服务 | 频次 | 置信 |
| --- | --- | ---: |
| member (`svc_member`) | 344 | med · **待核实** |
| pts (`svc_pts`) | 156 | high |
| fundout (`svc_fundout`) | 72 | high |
| acs (`svc_acs`) | 70 | high |
| cmf (`svc_cmf`) | 4 | high |

## 被调用方（←被调,本窗口观测）
(无)

## 观测到的对外方法
(无方法级证据)

## 同组服务（app_group=gp032，共 1 个模块）
- （本组仅此一个）
