---
id: scn_card_manage
object_type: Scenario
name: 绑卡管理 (Bank Cards)
aliases: []
domain: card
status: active
owner: jianfei.wang
reviewer: jianfei.wang
last_reviewed_at: '2026-06-24'
source_type: repo
source_ref: cgs-apitest/testcases/payment
tags: [card, cgs-apitest]
related_services: [svc_cards, svc_member]
related_tables: []
related_logs: []
---

# 绑卡管理 (Bank Cards)

> 业务测试场景。来源 cgs-apitest 回归。

## 场景描述
toC 银行卡管理:绑卡、查卡列表、解绑、卡校验等。经 cards 卡核心 + member。

## 关联关系
- **涉及服务**:[[svc_cards]]、[[svc_member]](= `related_services`)
- **覆盖的自动化**:见各 [[auto_*]]
- **读写的表**:待补

## 校验点(QA)
- 绑卡/解绑/查列表;卡敏感信息密文。
- 卡与会员绑定关系;落库卡状态。

## 来源与置信
- cgs-apitest 套件整理;服务链由调用线索+callgraph 推断,部分待补。
