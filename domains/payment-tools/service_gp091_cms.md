---
id: svc_cms
object_type: Service
domain: payment-tools
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp091
name: cms
dev_owner: Guoyou.Ma
aliases: [gp091_cms]
related_services: []
related_tables: []
---

# cms

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp091` · domain=`service-catalog`。

## 作用
内容 / 配置管理（被 remittance/member/trade/cashdesk 调用）

## 系统中的位置
- 功能层:客服 / 内容 / 查询 / 其他 (CS / Content / Query / Misc)
- 业务域:`service-catalog`

## 关联关系

**被调用(上游)—— 这些服务调用本服务:**
remittance, member, tradeii, cashdesk-api

## 参与的业务场景(cgs 回归)
- §2. 收银台 / 收银（`test_bpg_paypage` 收银侧、cashier 用例）
- §7. 跨境汇款（toC，`test_remittance`）
