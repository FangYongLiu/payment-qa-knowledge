---
id: domain_card
object_type: Domain
name: card
aliases: [卡]
domain: card
business_line: botim-money
status: active
owner: jianfei.wang
reviewer: jianfei.wang
last_reviewed_at: '2026-06-24'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: [card, 卡]
related_services: [svc_cards]
---

# card(卡)

> 业务域总览(入口节点)。owner jianfei.wang。细节见各服务对象。

## 概述
卡业务域:cards 卡核心能力。

## 覆盖范围
共 1 个服务:cards。

## QA 关注点
- 待补。

## 流程 / 场景 / 排障 索引
本域 流程 / 场景 / 排障 / 自动化 对象索引:
- [[flow_jaywan_prepaid_card]](流程:Jaywan 预付卡端到端流程(Dgpay 渠道))
- [[flow_ppc_card_lifecycle]](流程:PPC 卡端到端业务流程(开卡→激活→交易→清算→关卡))
- [[scn_card_lifecycle_transitions]](场景:PPC 卡生命周期状态转换测试场景集)
