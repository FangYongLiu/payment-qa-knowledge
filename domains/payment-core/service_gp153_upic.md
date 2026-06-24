---
id: svc_upic
object_type: Service
domain: payment-core
status: active
owner: unassigned
reviewer: unassigned
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp153
name: upic
dev_owner: Yu.Tang
aliases: [gp153_upic]
related_services: [svc_cms, svc_member, svc_pcs, svc_grc_check_identity_provider, svc_protocol]
related_tables: []
---

# upic

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp153` · domain=`service-catalog`。

## 作用
upic  **(据名推断 · 待核实:无作用文字证据,但下方有观测到的调用关系)**

## 系统中的位置
- 业务域:`service-catalog`

## 关联关系
**调用(下游)—— 本服务依赖:**
- [[svc_cms]] cms（内容 / 配置管理） · 3766 次 · high
- [[svc_member]] member（会员 / 账户核心） · 1732 次 · high
- [[svc_pcs]] pcs · 56 次 · high
- [[svc_grc_check_identity_provider]] grc-check-identity-provider（风控合规身份校验） · 42 次 · med·待核实
- [[svc_protocol]] protocol（代扣 / 签约协议管理） · 18 次 · high
