---
id: domain_lending
object_type: Domain
name: lending
aliases: [Quantix]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-06-24'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: [quantix, 信贷, paylater, 先买后付]
related_services: [svc_paylater, svc_credit_business, svc_cqm, svc_cbm, svc_botim_credit, svc_botim_snpl]
---

# quantix(信贷业务)

> 业务域总览。owner Xiaopei.Yan。本页是 quantix 域的入口节点,细节见各服务对象。

## 概述
Quantix 信贷 / 先买后付(BNPL)业务域:承载先买后付、信贷业务等借贷相关能力。

## 覆盖范围 / 部署 APP
- [[svc_paylater]](gp095,先买后付)、[[svc_credit_business]](gp130,信贷业务,调 member)、
  [[svc_cqm]](gp080)、[[svc_cbm]](gp081)。

## 关联关系
- **关键服务**:见上(4 个,dev_owner=Xiaopei.Yan)
- **下游依赖 / 关键流程 / 自动化资产**:待补(本窗口观测稀,待业务补充)。

## QA 关注点
- 待补(信贷额度 / 还款 / 风控联动等关注点留待补充)。