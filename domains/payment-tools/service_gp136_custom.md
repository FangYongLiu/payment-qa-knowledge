---
id: svc_custom
object_type: Service
domain: payment-tools
status: active
owner: unassigned
reviewer: unassigned
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp136
name: custom
dev_owner: Guoyou.Ma
aliases: [gp136_custom]
related_services: [svc_member]
related_tables: []
---

# custom

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp136` · domain=`service-catalog`。

## 作用
客户 / 定制配置（调 member；被 cashdesk 调用）

## 系统中的位置
- 功能层:客服 / 内容 / 查询 / 其他 (CS / Content / Query / Misc)
- 业务域:`service-catalog`

## 关联关系
**调用(下游)—— 本服务依赖:**
- [[svc_member]] member（会员 / 账户核心） · 4812 次 · high

**被调用(上游)—— 这些服务调用本服务:**
cashdesk-api

## 参与的业务场景(cgs 回归)
- §2. 收银台 / 收银（`test_bpg_paypage` 收银侧、cashier 用例）
