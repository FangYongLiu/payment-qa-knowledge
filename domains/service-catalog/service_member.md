---
id: svc_member
object_type: Service
domain: service-catalog
status: active
owner: unassigned
reviewer: unassigned
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp005
name: member
aliases: [gp005_member]
related_services: [svc_dpm_accounting, svc_ccdpm_accounting, svc_cms]
related_tables: []
---

# member

> 作用与调用关系来自 **UAT Kibana trace 观测**(2026-06-22T20:00Z..06-23T01:00Z UAT cgs 回归窗口,真实但**非穷尽**——
> 未被该窗口触达的调用不会出现)。**候选,待人审**(核心原则 #2)。app_group=`gp005`。

## 作用
会员 / 账户核心 —— 开户 / 查账户 / 校验支付密码 / 受益人（openAccount/checkPassword/queryAccountById），下游 dpm-accounting

## 下游调用（UAT trace 观测;observed_count=频次/权重）
| 被调服务 | 频次 | 置信 |
| --- | --- | ---: |
| dpm-accounting (`svc_dpm_accounting`) | 10913 | high |
| ccdpm-accounting (`svc_ccdpm_accounting`) | 607 | high |
| cms (`svc_cms`) | 26 | high |

## 被调用方（←被调,本窗口观测）
remittance, pfs-payment, reconciliation, credit-business, merchant-frontend, tradeii

## 观测到的对外方法
queryAccountById, queryMemberIntegratedInfo, openAccount, queryAccountByMemberId, checkPassword, queryBeneficiaryConfig

## 同组服务（app_group=gp005，共 1 个模块）
- （本组仅此一个）
